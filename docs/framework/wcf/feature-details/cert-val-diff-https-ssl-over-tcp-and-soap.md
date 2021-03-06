---
title: "Unterschiede bei der Zertifikatsvalidierung zwischen HTTPS, SSL über TCP und SOAP-Sicherheit"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords: certificates [WCF], validation differences
ms.assetid: 953a219f-4745-4019-9894-c70704f352e6
caps.latest.revision: "14"
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.workload: dotnet
ms.openlocfilehash: 34be2fbc5b8148d7bfdeb5e5d07e5b73ac89a97e
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="certificate-validation-differences-between-https-ssl-over-tcp-and-soap-security"></a>Unterschiede bei der Zertifikatsvalidierung zwischen HTTPS, SSL über TCP und SOAP-Sicherheit
Sie können in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] Zertifikate mit Sicherheit (SOAP) auf Nachrichtenebene neben der Transport Layer Security (TLS) über HTTP (HTTPS) oder TCP verwenden. In diesem Thema werden die Unterschiede bei der Überprüfung solcher Zertifikate beschrieben.  
  
## <a name="validation-of-https-client-certificates"></a>Validierung der HTTPS-Clientzertifikate  
 Wenn Sie HTTPS zur Kommunikation zwischen einem Client und einem Dienst verwenden, muss das Zertifikat, das der Client zur Authentifizierung für den Dienst verwendet, Vertrauensketten unterstützen. Es muss eine Verkettung zu einer vertrauenswerten Stammzertifizierungsstelle herstellen, anderenfalls gibt die HTTP-Ebene eine <xref:System.Net.WebException> mit der Meldung "Der Remoteserver hat einen Fehler zurückgegeben: (403) Unzulässig" aus. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] gibt diese Ausnahme als <xref:System.ServiceModel.Security.MessageSecurityException> aus.  
  
## <a name="validation-of-https-service-certificates"></a>Validierung der HTTPS-Dienstzertifikate  
 Wenn Sie HTTPS zur Kommunikation zwischen einem Client und einem Dienst verwenden, muss das Zertifikat, mit dem der Server die Authentifizierung durchführt, standardmäßig Vertrauensketten unterstützen. Es muss eine Verkettung zu einer vertrauenswerten Stammzertifizierungsstelle herstellen, Es wird keine Online-Überprüfung durchgeführt, um herauszufinden, ob das Zertifikat widerrufen wurde. Sie können dieses Verhalten auch überschreiben, indem Sie einen <xref:System.Net.Security.RemoteCertificateValidationCallback>-Rückruf registrieren, wie mit dem nachfolgenden Code dargestellt.  
  
 [!code-csharp[c_CertificateValidationDifferences#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_certificatevalidationdifferences/cs/source.cs#1)] 
 [!code-vb[c_CertificateValidationDifferences#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_certificatevalidationdifferences/vb/source.vb#1)]  
  
 Die Signatur für `ValidateServerCertificate` sieht folgendermaßen aus:  
  
 [!code-csharp[c_CertificateValidationDifferences#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_certificatevalidationdifferences/cs/source.cs#2)]
 [!code-vb[c_CertificateValidationDifferences#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_certificatevalidationdifferences/vb/source.vb#2)]  
  
 Durch die Implementierung des `ValidateServerCertificate` können beliebige Überprüfungen durchgeführt werden, die der Entwickler der Clientanwendung für notwendig erachtet, um das Dienstzertifikat zu überprüfen.  
  
## <a name="validation-of-client-certificates-in-ssl-over-tcp-or-soap-security"></a>Validierung der Clientzertifikate in SSL-über-TCP-Sicherheit oder SOAP-Sicherheit  
 Wenn Sie Secure Sockets Layer (SSL) über TCP oder die Nachrichtensicherheit (SOAP) verwenden, werden Clientzertifikate anhand des <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication.CertificateValidationMode%2A>-Eigenschaftswerts der <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication>-Klasse überprüft. Die Eigenschaft wird auf einen der <xref:System.ServiceModel.Security.X509CertificateValidationMode>-Werte festgelegt. Die Sperrüberprüfung kann anhand der Werte des <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication.RevocationMode%2A>-Eigenschaftswerts der <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication>-Klasse durchgeführt werden. Die Eigenschaft wird auf einen der <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode>-Werte festgelegt.  
  
 [!code-csharp[c_CertificateValidationDifferences#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_certificatevalidationdifferences/cs/source.cs#3)]
 [!code-vb[c_CertificateValidationDifferences#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_certificatevalidationdifferences/vb/source.vb#3)]  
  
## <a name="validation-of-service-certificate-in-ssl-over-tcp-and-soap-security"></a>Validierung der Dienstzertifikate in SSL-über-TCP-Sicherheit und SOAP-Sicherheit  
 Wenn Sie SSL über TCP oder die (SOAP)-Nachrichtensicherheit verwenden, werden Dienstzertifikate anhand des <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CertificateValidationMode%2A>-Eigenschaftswerts der <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication>-Klasse überprüft. Die Eigenschaft wird auf einen der <xref:System.ServiceModel.Security.X509CertificateValidationMode>-Werte festgelegt.  
  
 Die Sperrüberprüfung kann anhand der Werte des <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.RevocationMode%2A>-Eigenschaftswerts der <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication>-Klasse durchgeführt werden. Die Eigenschaft wird auf einen der <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode>-Werte festgelegt.  
  
 [!code-csharp[c_CertificateValidationDifferences#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_certificatevalidationdifferences/cs/source.cs#4)]
 [!code-vb[c_CertificateValidationDifferences#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_certificatevalidationdifferences/vb/source.vb#4)]  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Net.Security.RemoteCertificateValidationCallback>  
 [Arbeiten mit Zertifikaten](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)
