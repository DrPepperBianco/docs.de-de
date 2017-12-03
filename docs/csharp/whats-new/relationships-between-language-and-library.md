---
title: Die Beziehung zwischen den Funktionen der Programmiersprache und Bibliothekstypen | Microsoft Docs
description: "Sprachfunktionen basieren häufig auf Bibliothekstypen für die Implementierung. Diese Beziehung zu verstehen."
keywords: C#-Sprachentwurf-Standardbibliothek
author: billwagner
ms.author: wiwagn
ms.date: 07/20/2017
ms.topic: article
ms.prod: .net
ms.devlang: devlang-csharp
ms.openlocfilehash: 93fd26a72743fcf45df3904cb8d0c787d8a228a8
ms.sourcegitcommit: bbde43da655ae7bea1977f7af7345eb87bd7fd5f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/21/2017
---
# <a name="relationships-between-language-features-and-library-types"></a><span data-ttu-id="f56b1-105">Beziehungen zwischen den Funktionen der Programmiersprache und Bibliothekstypen</span><span class="sxs-lookup"><span data-stu-id="f56b1-105">Relationships between language features and library types</span></span>

<span data-ttu-id="f56b1-106">Der C#-Sprachendefinition erfordert eine Standardbibliothek auf bestimmte Typen und bestimmte zugängliche Member für diese Typen verfügen.</span><span class="sxs-lookup"><span data-stu-id="f56b1-106">The C# language definition requires a standard library to have certain types and certain accessible members on those types.</span></span> <span data-ttu-id="f56b1-107">Der Compiler generiert Code, der diese erforderlichen Typen und Member für viele verschiedene Sprachfunktionen verwendet.</span><span class="sxs-lookup"><span data-stu-id="f56b1-107">The compiler generates code that uses these required types and members for many different language features.</span></span> <span data-ttu-id="f56b1-108">Falls erforderlich, stehen die NuGet-Pakete, die enthalten Typen, die für neuere Versionen der Sprache benötigt wird, wenn die Schreiben von Code für Umgebungen, in denen diese Typen oder Member nicht noch bereitgestellt wurden.</span><span class="sxs-lookup"><span data-stu-id="f56b1-108">When necessary, there are NuGet packages that contain types needed for newer versions of the language when writing code for environments where those types or members have not been deployed yet.</span></span>

<span data-ttu-id="f56b1-109">Dieser Abhängigkeit von Funktionen der Standardbibliothek wurde Teil der C#-Sprache seit der ersten Version.</span><span class="sxs-lookup"><span data-stu-id="f56b1-109">This dependency on standard library functionality has been part of the C# language since its first version.</span></span> <span data-ttu-id="f56b1-110">In dieser Version enthalten Beispiele:</span><span class="sxs-lookup"><span data-stu-id="f56b1-110">In that version, examples included:</span></span>

* <span data-ttu-id="f56b1-111"><xref:System.Exception>– verwendet für alle vom Compiler generierte Ausnahmen.</span><span class="sxs-lookup"><span data-stu-id="f56b1-111"><xref:System.Exception> - used for all compiler generated exceptions.</span></span>
* <span data-ttu-id="f56b1-112"><xref:System.String>-die C#- `string` Typ ist ein Synonym für <xref:System.String>.</span><span class="sxs-lookup"><span data-stu-id="f56b1-112"><xref:System.String> - the C# `string` type is a synonym for <xref:System.String>.</span></span>
* <span data-ttu-id="f56b1-113"><xref:System.Int32>-Synonym für `int`.</span><span class="sxs-lookup"><span data-stu-id="f56b1-113"><xref:System.Int32> - synonym of `int`.</span></span>

<span data-ttu-id="f56b1-114">Diese erste Version war einfach: der Compiler und die Standardbibliothek geliefert zusammen, und es wurde nur eine Version der einzelnen.</span><span class="sxs-lookup"><span data-stu-id="f56b1-114">That first version was simple: the compiler and the standard library shipped together, and there was only one version of each.</span></span>

<span data-ttu-id="f56b1-115">Nachfolgende Versionen von c# haben gelegentlich neue Typen oder Member Abhängigkeiten hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="f56b1-115">Subsequent versions of C# have occasionally added new types or members to the dependencies.</span></span> <span data-ttu-id="f56b1-116">Beispiele hierfür sind: <xref:System.Runtime.CompilerServices.INotifyCompletion>, <xref:System.Runtime.CompilerServices.CallerFilePathAttribute> und <xref:System.Runtime.CompilerServices.CallerMemberNameAttribute>.</span><span class="sxs-lookup"><span data-stu-id="f56b1-116">Examples include: <xref:System.Runtime.CompilerServices.INotifyCompletion>, <xref:System.Runtime.CompilerServices.CallerFilePathAttribute> and <xref:System.Runtime.CompilerServices.CallerMemberNameAttribute>.</span></span> <span data-ttu-id="f56b1-117">C#-7.0 weiterhin dies durch Hinzufügen einer Abhängigkeit auf <xref:System.ValueTuple> zum Implementieren der [Tupel](../tuples.md) Sprachfunktion.</span><span class="sxs-lookup"><span data-stu-id="f56b1-117">C# 7.0 continues this by adding a dependency on <xref:System.ValueTuple> to implement the [tuples](../tuples.md) language feature.</span></span>

<span data-ttu-id="f56b1-118">Das Entwurfsteam Sprache funktioniert auf um die Typen und Member, die in eine kompatible Standardbibliothek erforderlich die Angriffsfläche zu reduzieren.</span><span class="sxs-lookup"><span data-stu-id="f56b1-118">The language design team works to minimize the surface area of the types and members required in a compliant standard library.</span></span> <span data-ttu-id="f56b1-119">Das Ziel wird für eine fehlerfreie Entwurf verteilt, auf dem neuen Bibliotheksfunktionen nahtlos in die Sprache integriert sind.</span><span class="sxs-lookup"><span data-stu-id="f56b1-119">That goal is balanced against a clean design where new library features are incorporated seamlessly into the language.</span></span> <span data-ttu-id="f56b1-120">Es werden neue Funktionen in zukünftigen Versionen von c#, die erfordern neue Typen und Member in eine Standardbibliothek.</span><span class="sxs-lookup"><span data-stu-id="f56b1-120">There will be new features in future versions of C# that require new types and members in a standard library.</span></span> <span data-ttu-id="f56b1-121">Es ist wichtig zu verstehen, wie diese Abhängigkeiten in Ihre Arbeit zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="f56b1-121">It's important to understand how to manage those dependencies in your work.</span></span>

## <a name="managing-your-dependencies"></a><span data-ttu-id="f56b1-122">Verwalten Ihre Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="f56b1-122">Managing your dependencies</span></span>

<span data-ttu-id="f56b1-123">C#-Compiler-Tools werden jetzt von den Freigabezyklus der Bibliotheken .NET auf unterstützten Plattformen entkoppelt.</span><span class="sxs-lookup"><span data-stu-id="f56b1-123">C# compiler tools are now decoupled from the release cycle of the .NET libraries on supported platforms.</span></span> <span data-ttu-id="f56b1-124">Tatsächlich haben unterschiedliche .NET Bibliotheken unterschiedliche Versionszyklen: .NET Framework auf Windows Relesed als Windows Update, .NET Core auf einem separaten Zeitplan, und die Xamarin-Versionen der Bibliothek die Updates im Lieferumfang der Xamarin-Tools für jede Zielplattform geliefert wird.</span><span class="sxs-lookup"><span data-stu-id="f56b1-124">In fact, different .NET libraries have different release cycles: the .NET Framework on Windows is relesed as a Windows Update, .NET Core ships on a separate schedule, and the Xamarin versions of library updates ship with the Xamarin tools for each target platform.</span></span>

<span data-ttu-id="f56b1-125">Sie wird nicht den Großteil der Optimierungszeit, diese Änderungen beachten.</span><span class="sxs-lookup"><span data-stu-id="f56b1-125">The majority of time, you won't notice these changes.</span></span> <span data-ttu-id="f56b1-126">Allerdings bei der Arbeit mit einer neueren Version der Sprache, die Features nicht erfordert noch in der .NET-Bibliotheken für diese Plattform, verweisen die NuGet-Pakete zum Bereitstellen dieser neuen Typen.</span><span class="sxs-lookup"><span data-stu-id="f56b1-126">However, when you are working with a newer version of the language that requires features not yet in the .NET libraries on that platform, you'll reference the NuGet packages to provide those new types.</span></span>
<span data-ttu-id="f56b1-127">Die Plattformen, die Ihre app unterstützt bei Neuinstallationen Framework aktualisiert werden, können Sie den zusätzlichen Verweis entfernen.</span><span class="sxs-lookup"><span data-stu-id="f56b1-127">As the platforms your app supports are updated with new framework installations, you can remove the extra reference.</span></span>

<span data-ttu-id="f56b1-128">Diese Trennung bedeutet, dass Sie neue Sprachfeatures verwenden können, selbst wenn Sie Computer, die möglicherweise keine entsprechende Framework abzielen.</span><span class="sxs-lookup"><span data-stu-id="f56b1-128">This separation means you can use new language features even when you are targeting machines that may not have the corresponding framework.</span></span>