---
title: Overview and workflow of using NuGet packages | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: null
description: An overview of the process of consuming NuGet packages in a project, with links to other specific parts of the process.
keywords: NuGet package consumption, NuGet consumption overview, NuGet consumption workflow, package consumption workflow, package consumption overview
ms.reviewer:
- karann-msft
- unniravindranathan
---

# Package consumption workflow

Between nuget.org and private package galleries that your organization might establish, you can find tens of thousands of highly useful packages to use in your apps and services. But regardless of the source, consuming a package follows the same general workflow as shown below. For details, see [Finding and Choosing Packages](../consume-packages/finding-and-choosing-packages.md) and [Different ways to install a NuGet package](ways-to-install-a-package.md).

![Flow of going to a package source, finding a package, installing it in a project, then adding a using statement and calls to the package API](media/Overview-01-GeneralFlow.png)

\* _Except with `nuget install` from the command-line, in which case it's necessary to edit the configuration files by hand. See the [install command reference](../tools/cli-ref-install.md)._

NuGet remembers the identity and version number of each installed package, recording it in either `packages.config` or the project file, depending on project type and your version of NuGet. With NuGet 4.0+, [storing dependencies in the project file, or PackageReference](../consume-packages/package-references-in-project-files.md) is generally the default, although this is configurable in Visual Studio through the [Package Manager UI options](../tools/package-manager-ui.md). In any case, you can look in the appropriate file at any time to see the full list of dependencies for your project.

> [!Tip]
> It's prudent to always check the license for each package you intend to use in your software. On nuget.org, you find a **License Info** link on the right side of each package's description page. If a package does not specify license terms, contact the package owner directly using the **Contact owners** link on the package page. Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.

When installing packages, NuGet typically checks if the package is already available from its cache. You can manually clear this cache from the command line, as described on [Managing the NuGet cache](../consume-packages/managing-the-nuget-cache.md).

NuGet also makes sure that the target frameworks supported by the package are compatible with your project. If the package does not contain compatible assemblies, NuGet will give you an error message. See [Resolving incompatible package errors](dependency-resolution.md#resolving-incompatible-package-errors).

When adding project code to a source repository, you typically don't include NuGet packages. Those who later clone the repository, which includes build agents on systems like Visual Studio Team Services, must restore the necessary packages prior to running a build:

![Flow of restoring NuGet packages by cloning a repository and using either a restore command](media/Overview-02-RestoreFlow.png)

[Package Restore](../consume-packages/package-restore.md) uses the information in the project file or `packages.config` to reinstall all dependencies. Note that there are differences in the process involved, as described in [Dependency Resolution](../consume-packages/dependency-resolution.md).

Occasionally it's necessary to reinstall packages that are already included in a project, which may also reinstall dependencies. This is easy to do using the `reinstall` command via the NuGet command line or the NuGet Package Manager Console. For details, see [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md).

Finally, NuGet's behavior is driven by `Nuget.Config` configuration files. Multiple files can be used to centralize certain settings at different levels, as explained in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).

Enjoy your productive coding with NuGet packages!
