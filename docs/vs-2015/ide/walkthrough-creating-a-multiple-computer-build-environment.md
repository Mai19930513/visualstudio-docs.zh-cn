---
title: 演练：创建多计算机生成环境 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, building on multiple computers
- build environment, MSBuild
ms.assetid: ae5391b1-3eec-42f5-beb3-f28630615a9e
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7d0fccb5694e538cdf71844d2cc18640114ec735
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672313"
---
# <a name="walkthrough-creating-a-multiple-computer-build-environment"></a>演练：创建多计算机生成环境
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以在组织内创建生成环境，方式为在主计算机上安装 Visual Studio，然后将各种文件和设置复制到其他计算机以便 Visual Studio 参与生成。 您不必在另一台计算机上安装 Visual Studio。

 本文档未授予在外部重新分布软件或向第三方提供生成环境的权利。

||
|-|
|免责声明<br /><br /> 本文档是“按原样”提供的。 虽然我们已测试概述的步骤，但无法全面彻底地测试每一个配置。 我们将尝试保持文档与了解到的任何其他信息保持最新。 本文档中表达的信息和观点（包括 URL 和其他 Internet 网站引用）如有更改，恕不另行通知。 Microsoft 对此处提供的信息不提供任何明示或暗示的保证。 您自行承担其使用风险。<br /><br /> 本文档未向您提供任何 Microsoft 产品中任何知识产权的任何合法权利。 您可为了内部参考目的复制和使用本文档。<br /><br /> 您没有义务为 Microsoft 提供有关本文档的任何建议、评论或其他反馈（以下简称“反馈”）。 但是，可能在 Microsoft 产品和相关规范或其他文档（统称为“Microsoft 服务内容”）中使用您自愿提供的任何反馈，其他第三方可能反过来依赖这些内容来开发其自己的产品。 因此，如果您为 Microsoft 提供有关本文档任何形式或有关其适用于的 Microsoft 服务内容的反馈，则您同意：(a) Microsoft 可自由使用、重现、许可、分发您的反馈以及以其他方式使您的反馈在任何 Microsoft 服务内容中商业化；(b) 您还免费授予第三方权利，仅限于支持其他产品与吸收了您的反馈的 Microsoft 产品的任何特定部分结合使用或交互所需的专利权；以及 (c) 您不会向 Microsoft 提供任何符合下列条件的反馈 (i) 您有理由认为受任何第三方的任何专利、版权或其他知识产权或声明约束；或 (ii) 受追求需要任何 Microsoft 服务内容吸收或派生自此类反馈的许可条款、或要授予许可或以其他方式与任何第三方共享的其他 Microsoft 知识产权约束。|

 已通过在命令行上执行 MSBuild 和通过使用 Team Foundation Build 对下列操作系统验证了此演练。

- Windows 8（x86 和 x64）

- Windows 7 Ultimate

- Windows Server 2008 R2 Standard

  在完成此演练中的步骤之后，您可使用多计算机环境生成下列类型的应用程序：

- 使用 Windows 8 SDK 的 C++ 桌面应用程序

- 面向 .NET Framework 4.5 的 Visual Basic 或 C# 桌面应用程序

  多计算机环境不能用于生成下列类型的应用程序：

- [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)]应用。 若要生成 [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)]应用，您必须在生成计算机上安装 Visual Studio。

- 面向 .NET Framework 4 或更早版本的桌面应用程序。 若要生成这些类型的应用程序，您必须在生成计算机上安装 Visual Studio 或 .NET 引用程序集和工具（通过 Windows 7.1 SDK）。

  此演练分为下列部分：

- [在计算机上安装软件](../ide/walkthrough-creating-a-multiple-computer-build-environment.md#InstallingSoftware)

- [将文件从主计算机复制到生成计算机](../ide/walkthrough-creating-a-multiple-computer-build-environment.md#CopyingFiles)

- [正在创建注册表设置](../ide/walkthrough-creating-a-multiple-computer-build-environment.md#CreatingRegistry)

- [在生成计算机上设置环境变量](../ide/walkthrough-creating-a-multiple-computer-build-environment.md#SettingEnvVariables)

- [将 MSBuild 程序集安装到生成计算机上的全局程序集缓存 (GAC) ](../ide/walkthrough-creating-a-multiple-computer-build-environment.md#InstallingMSBuildToGAC)

- [生成项目](../ide/walkthrough-creating-a-multiple-computer-build-environment.md#BuildingProjects)

- [创建可以签入源代码管理的生成环境](../ide/walkthrough-creating-a-multiple-computer-build-environment.md#CreatingForSourceControl)

## <a name="prerequisites"></a>先决条件

- Visual Studio Ultimate、Visual Studio Premium 或 Visual Studio Professional 的许可副本

- .NET Framework 4.5.1 的副本，可以从 [Microsoft](https://www.microsoft.com/download/details.aspx?id=40779) 网站下载。

## <a name="installing-software-on-the-computers"></a><a name="InstallingSoftware"></a> 在计算机上安装软件
 首先，先后设置主计算机和生成计算机。

 通过在主计算机上安装 Visual Studio，创建之后将复制到生成计算机的文件和设置。 您可在 x86 或 x64 计算机上安装 Visual Studio，但生成计算机的体系结构必须与主计算机的体系结构匹配。

#### <a name="to-install-software-on-the-computers"></a>在计算机上安装软件

1. 在主计算机上安装 Visual Studio。

2. 在生成计算机上，安装 .NET Framework 4.5。 若要验证是否已安装，请确保注册表项 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full@Version 的值以“4.5”开头。

## <a name="copying-files-from-the-host-computer-to-the-build-computer"></a><a name="CopyingFiles"></a>将文件从主计算机复制到生成计算机
 本节包括将特定文件、编译器、生成工具、MSBuild 资产和注册表设置从主计算机复制到生成计算机。 这些说明假定，您已在主计算机的默认位置安装了 Visual Studio；如果安装在其他位置，请相应地调整步骤。

- 在 x86 计算机上，默认位置为 C:\Program Files\Microsoft Visual Studio 11.0\

- 在 x64 计算机上，默认位置为 C:\Program Files (x86)\Microsoft Visual Studio 11.0\

  请注意，Program Files 文件夹的名称取决于所安装的操作系统。 在 x86 计算机上，名称为 \Program Files\\；在 x64 计算机上，名称为 \Program Files (x86)\\。 不考虑系统体系结构，此演练中的 Program Files 文件夹指的是 %ProgramFiles%。

> [!NOTE]
> 在生成计算机上，所有相关文件必须位于同一驱动器上；但是，该驱动器的驱动器号可能与主计算机上安装 Visual Studio 的驱动器的驱动器号不同。 在任何情况下，您在创建注册表项时，必须考虑文件位置，如本文档下文所述。

#### <a name="to-copy-the-windows-sdk-files-to-the-build-computer"></a>将 Windows SDK 文件复制到生成计算机

1. 如果您仅安装了 Windows SDK for Windows 8，请从主计算机将这些文件夹复制到生成计算机：

   - %ProgramFiles%\Windows Kits\8.0\bin\

   - %ProgramFiles%\Windows Kits\8.0\Catalogs\

   - %ProgramFiles%\Windows Kits\8.0\DesignTime\

   - %ProgramFiles%\Windows Kits\8.0\include\

   - %ProgramFiles%\Windows Kits\8.0\Lib\

   - %ProgramFiles%\Windows Kits\8.0\Redist\

   - %ProgramFiles%\Windows Kits\8.0\References\

     如果您还有其他 Windows 8 工具包…

   - Microsoft Windows 评估和部署工具包

   - Microsoft Windows 驱动程序工具包

   - Microsoft Windows 硬件认证工具包

     ...它们可能已将文件安装到上一步列出的 %ProgramFiles%\Windows Kits\8.0\ 文件夹中，并且其许可条款可能不允许这些文件的生成服务器权利。 查看安装的每个 Windows 工具包的许可条款以验证文件是否可复制到生成计算机。 如果许可条款不允许生成服务器权利，则将从生成计算机删除这些文件。

2. 将下列文件夹以递归方式从主计算机复制到生成计算机：

   - %ProgramFiles%\Microsoft SDKs\Windows\v8.0A\bin\NETFX 4.0 Tools\

   - %ProgramFiles%\Common Files\Merge Modules\

   - %ProgramFiles%\Microsoft Visual Studio 11.0\VC\

   - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\Tools\ProjectComponents\

   - %ProgramFiles%\MSBuild\Microsoft.Cpp\v4.0\V110\

   - %ProgramFiles%\Reference Assemblies\Microsoft\Framework\\.NETCore\v4.5\

   - %ProgramFiles%\Reference Assemblies\Microsoft\Framework\\.NETFramework\v4.5\

3. 从这些文件从主计算机复制到生成计算机：

   - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE\msobj110.dll

   - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE\mspdb110.dll

   - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE\mspdbcore.dll

   - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE\mspdbsrv.exe

   - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE\msvcdis110.dll

   - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\Tools\makehm.exe

   - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\Tools\VCVarsQueryRegistry.bat

   - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\Tools\vsvars32.bat

4. 仅当您在生成计算机上运行生成输出时才需要下列 Visual C++ 运行库 - 例如，作为自动测试的一部分。 这些文件一般位于 %ProgramFiles%\Microsoft Visual Studio 11.0\VC\redist\x86\ 或 %ProgramFiles%\Microsoft Visual Studio 11.0\VC\redist\x64\ 文件夹下的子文件夹，具体取决于系统体系结构。 在 x86 系统中，将 x86 二进制文件复制到 \Windows\System32\ 文件夹。 在 x64 系统中，将 x86 二进制文件复制到 Windows\SysWOW64\ 文件夹，并将 x64 二进制文件复制到 Windows\System32\ 文件夹。

   - \Microsoft.VC110.ATL\atl110.dll

   - \Microsoft.VC110.CRT\msvcp110.dll

   - \Microsoft.VC110.CRT\msvcr110.dll

   - \Microsoft.VC110.CXXAMP\vcamp110.dll

   - \Microsoft.VC110.MFC\mfc110.dll

   - \Microsoft.VC110.MFC\mfc110u.dll

   - \Microsoft.VC110.MFC\mfcm110.dll

   - \Microsoft.VC110.MFC\mfcm110u.dll

   - \Microsoft.VC110.MFCLOC\mfc110chs.dll

   - \Microsoft.VC110.MFCLOC\mfc110cht.dll

   - \Microsoft.VC110.MFCLOC\mfc110deu.dll

   - \Microsoft.VC110.MFCLOC\mfc110enu.dll

   - \Microsoft.VC110.MFCLOC\mfc110esn.dll

   - \Microsoft.VC110.MFCLOC\mfc110fra.dll

   - \Microsoft.VC110.MFCLOC\mfc110ita.dll

   - \Microsoft.VC110.MFCLOC\mfc110jpn.dll

   - \Microsoft.VC110.MFCLOC\mfc110kor.dll

   - \Microsoft.VC110.MFCLOC\mfc110rus.dll

   - \Microsoft.VC110.OPENMP\vcomp110.dll

5. 只将下列文件从 \Debug_NonRedist\x86\ 或 \Debug_NonRedist\x64\ 文件夹复制到生成计算机，如[准备用于运行调试可执行文件的测试计算机](/cpp/windows/preparing-a-test-machine-to-run-a-debug-executable)中所述。 无其他文件可复制。

   - \Microsoft.VC110.DebugCRT\msvcp110d.dll

   - \Microsoft.VC110.DebugCRT\msvcr110d.dll

   - \Microsoft.VC110.DebugCXXAMP\vcamp110d.dll

   - \Microsoft.VC110.DebugMFC\mfc110d.dll

   - \Microsoft.VC110.DebugMFC\mfc110ud.dll

   - \Microsoft.VC110.DebugMFC\mfcm110d.dll

   - \Microsoft.VC110.DebugMFC\mfcm110ud.dll

   - \Microsoft.VC110.DebugOpenMP\vcomp110d.dll

## <a name="creating-registry-settings"></a><a name="CreatingRegistry"></a>创建注册表设置
 您必须创建注册表项才能配置 MSBuild 的设置。

#### <a name="to-create-registry-settings"></a>创建注册表设置

1. 标识注册表项的父文件夹。 所有注册表项均是在同一父项下创建的。 在 x86 计算机上，父项为 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\。 在 x64 计算机上，父项为 HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\。 不考虑系统体系结构，此演练中的父项指的是 %RegistryRoot%。

   > [!NOTE]
   > 如果您的主计算机体系结构与您的生成计算机的不同，则请确保在每台计算机上使用适当的父项。 这在您实现导出过程的自动化时尤其重要。
   >
   >  此外，如果您在生成计算机上使用的驱动器号不同于在主计算机上使用的，则请确保更改注册表项的值以匹配。

2. 在生成计算机上创建下列注册表项。 所有这些项都是字符串（在注册表中类型为“REG_SZ”）。 将这些项的值设置为与主计算机上可比较项的值相同。

   - %RegistryRoot%\\.NETFramework\v4.0.30319\AssemblyFoldersEx\VCMSBuild Public Assemblies@(Default)

   - %RegistryRoot%\Microsoft SDKs\Windows\v8.0@InstallationFolder

   - %RegistryRoot%\Microsoft SDKs\Windows\v8.0A@InstallationFolder

   - %RegistryRoot%\Microsoft SDKs\Windows\v8.0A\WinSDK-NetFx40Tools@InstallationFolder

   - %RegistryRoot%\Microsoft SDKs\Windows\v8.0A\WinSDK-NetFx40Tools-x86@InstallationFolder

   - %Registryroot%\VisualStudio\11.0@Source 目录

   - %RegistryRoot%\VisualStudio\11.0\Setup\VC@ProductDir

   - %RegistryRoot%\VisualStudio\SxS\VC7@FrameworkDir32

   - %RegistryRoot%\VisualStudio\SxS\VC7@FrameworkDir64

   - %RegistryRoot%\VisualStudio\SxS\VC7@FrameworkVer32

   - %RegistryRoot%\VisualStudio\SxS\VC7@FrameworkVer64

   - %RegistryRoot%\VisualStudio\SxS\VC7@11.0

   - %RegistryRoot%\VisualStudio\SxS\VS7@11.0

   - %RegistryRoot%\Windows Kits\Installed Roots@KitsRoot

   - %RegistryRoot%\MSBuild\ToolsVersions\4.0\11.0@VCTargetsPath

   - %RegistryRoot%\MSBuild\ToolsVersions\4.0\11.0@VCTargetsPath10

   - %RegistryRoot%\MSBuild\ToolsVersions\4.0\11.0@VCTargetsPath11

     在 x64 生成计算机上，同样创建以下注册表项并参考主计算机来确定如何设置。

   - %RegistryRoot%\Microsoft SDKs\Windows\v8.0A\WinSDK-NetFx40Tools-x64@InstallationFolder

     如果你的生成计算机为 x64 并且你要使用 64 位版本的 MSBuild，或者你要在 x64 计算机上使用 Team Foundation Server Build Service，则必须在本机 64 位注册表中创建下列注册表项。 请参见主计算机来确定如何设置这些项。

   - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\11.0\Setup\VS@ProductDir

   - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSBuild\ToolsVersions\4.0\11.0@VCTargetsPath

   - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSBuild\ToolsVersions\4.0\11.0@VCTargetsPath10

   - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSBuild\ToolsVersions\4.0\11.0@VCTargetsPath11

## <a name="setting-environment-variables-on-the-build-computer"></a><a name="SettingEnvVariables"></a> 在生成计算机上设置环境变量
 若要在生成计算机上使用 MSBuild，则必须设置 PATH 环境变量。 您可以使用 vcvarsall.bat 设置变量，也可以手动配置它们。

#### <a name="to-use-vcvarsallbat-to-set-environment-variables"></a>使用 vcvarsall.bat 设置环境变量

- 在生成计算机上打开“命令提示符”窗口，运行 %Program Files%\Microsoft Visual Studio 11.0\VC\vcvarsall.bat。 您可以使用命令行参数指定要使用的工具集 - x86、本机 x64 或 x64 交叉编译器。 如果未指定命令行参数，则使用 x86 工具集。

     下表描述了 vcvarsall.bat 支持的参数：

    |Vcvarsall.bat 参数|编译器|生成计算机体系结构|生成输出体系结构|
    |----------------------------|--------------|---------------------------------|-------------------------------|
    |x86（默认）|32 位本机|x86、x64|x86|
    |x86_amd64|x64 兼容|x86、x64|X64|
    |amd64|x64 本机|X64|X64|

     如果 vcvarsall.bat 运行成功（即，不显示任何错误消息），可以跳过下一步，继续执行本文的[将 MSBuild 程序集安装到生成计算机上的全局程序集缓存 (GAC) 中](../ide/walkthrough-creating-a-multiple-computer-build-environment.md#InstallingMSBuildToGAC)部分中的步骤。

#### <a name="to-manually-set-environment-variables"></a>手动设置环境变量

1. 若要手动配置命令行环境，请将此路径添加到 PATH 环境变量：

   - %Program Files%\Microsoft Visual Studio 11.0\Common7\IDE

2. 您也可以将下列路径添加到 PATH 变量以使得使用 MSBuild 生成解决方案更容易。

    如果要使用本机 32 位 MSBuild，请将下列路径添加到 PATH 变量中：

   - %Program Files%\Microsoft SDKs\Windows\v8.0A\bin\NETFX 4.0 Tools

   - %windir%\Microsoft.NET\Framework\v4.0.30319

     如果要使用本机 64 位 MSBuild，请将下列路径添加到 PATH 变量：

   - %Program Files%\Microsoft SDKs\Windows\v8.0A\bin\NETFX 4.0 Tools\x64

   - %windir%\Microsoft.NET\Framework64\v4.0.30319

## <a name="installing-msbuild-assemblies-to-the-global-assembly-cache-gac-on-the-build-computer"></a><a name="InstallingMSBuildToGAC"></a>将 MSBuild 程序集安装到生成计算机上的全局程序集缓存 (GAC) 中
 MSBuild 需要在生成计算机的 GAC 上安装一些附加程序集。

#### <a name="to-copy-assemblies-from-the-host-computer-and-install-them-on-the-build-computer"></a>从主计算机复制程序集并在生成计算机上安装它们

1. 从主计算机将下列程序集复制到生成计算机。 由于它们将安装到 GAC，因此将其放置在生成计算机上的什么位置并不重要。

    - %ProgramFiles%\MSBuild\Microsoft.Cpp\v4.0\v110\Microsoft.Build.CPPTasks.Common.v110.dll

    - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE\CommonExtensions\Microsoft\VC\Project\Microsoft.VisualStudio.Project.VisualC.VCProjectEngine.dll

    - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE\PublicAssemblies\Microsoft.VisualStudio.VCProjectEngine.dll

2. 若要将程序集安装到 GAC 中，请在生成计算机上查找 gacutil.exe（一般位于 %ProgramFiles%\Microsoft SDKs\Windows\v8.0A\bin\NETFX 4.0 Tools\\ 中）。 如果找不到此文件夹，请重复执行本演练的[将文件从主计算机复制到生成计算机](../ide/walkthrough-creating-a-multiple-computer-build-environment.md#CopyingFiles)部分中的步骤。

     打开具有管理权限的“命令提示符”窗口，针对每个文件运行以下命令：

     **gacutil.exe-i \<file>**

    > [!NOTE]
    > 若要将程序集完全安装到 GAC 中，可能需要重新启动。

## <a name="building-projects"></a><a name="BuildingProjects"></a> 生成项目
 您可以使用 Team Foundation Build 生成 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] 项目和解决方案，也可以在命令行上生成它们。 当您使用 Team Foundation Build 生成项目时，将调用对应于系统体系结构的 MSBuild 可执行文件。  在命令行上，您可以使用 32 位 MSBuild 或 64 位 MSBuild，并且您可以通过设置 PATH 环境变量或通过直接调用特定于体系结构的 MSBuild 可执行文件来选择 MSBuild 的体系结构。

 若要在命令提示符处使用 msbuild.exe，请运行以下命令，其中 solution.sln 是解决方案名称的占位符**。

 **msbuild** *solution.sln*

 有关如何在命令行上使用 MSBuild 的详细信息，请参阅 [命令行参考](../msbuild/msbuild-command-line-reference.md)。

> [!NOTE]
> 若要生成 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] 项目，您必须使用“v110”平台工具集。 如果您不想编辑 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] 项目文件，则可以使用此命令行参数来设置平台工具集：
>
> **msbuild** *solution.sln* **/p:PlatformToolset=v110**

## <a name="creating-the-build-environment-so-that-it-can-be-checked-into-source-control"></a><a name="CreatingForSourceControl"></a> 创建生成环境，以便可以将其签入源代码管理
 您可以创建可部署到不同计算机的生成环境，这不需要 GAC 文件，也不需要修改注册表设置。 下列步骤只是实现此目的的一种途径。 使这些步骤适应您的生成环境的独特特征。

> [!NOTE]
> 您必须禁用增量生成，以便 tracker.exe 不会在生成期间引发错误。 若要禁用增量生成，请设置此生成参数：
>
> **msbuild** *solution.sln* **/p:TrackFileAccess=false**

#### <a name="to-create-a-build-environment-that-can-be-checked-into-source-control"></a>创建可签入源代码管理的生成环境

1. 在主计算机上创建“Depot”目录。

     此目录在这些步骤中指的是 %Depot%。

2. 复制目录和文件，大致就像本演练的[将文件从主计算机复制到生成计算机](../ide/walkthrough-creating-a-multiple-computer-build-environment.md#CopyingFiles)部分所述，不同之处在于要将它们粘贴到刚刚创建的 %Depot% 目录下。 例如，从 %ProgramFiles%\Windows Kits\8.0\bin\ 复制到 %Depot%\Windows Kits\8.0\bin\\。

3. 如果在 %Depot% 中粘贴文件，则请进行下列更改：

    - 在 %Depot%\MSBuild\Microsoft.Cpp\v4.0\v110\Microsoft.CPP.Targets、\Microsoft.Cpp.InvalidPlatforms.targets\\、\Microsoft.cppbuild.targets\\ 和 \Microsoft.CppCommon.targets\\ 中，将 

         AssemblyName="Microsoft.Build.CppTasks.Common.v110, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a" 的每个实例

         to

         AssemblyFile="$(VCTargetsPath11)Microsoft.Build.CppTasks.Common.v110.dll"。

         以前的命名依赖 GAC 程序集。

    - 在 %Depot% \MSBuild\Microsoft.Cpp\v4.0\v110\Microsoft.CPPClean.Targets 中，将以下内容的每个实例

         AssemblyName="Microsoft.Build.CppTasks.Common.v110, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a" 的每个实例

         to

         AssemblyFile="$(VCTargetsPath11)Microsoft.Build.CppTasks.Common.v110.dll"。

4. 创建 .props 文件（例如，Partner.AutoImports.props），将其放入包含您的项目的根文件夹中。 此文件将用于设置 MSBuild 用于查找各种资源的变量。 如果变量不是此文件设置的，则它们是其他依赖注册表值的 .props 文件和 .targets 文件设置的。 由于我们不会设置任何注册表值，因此这些变量将为空，并且生成将失败。 请将此添加到 Partner.AutoImports.props：

    ```
    <?xml version="1.0" encoding="utf-8"?>
    <!-- This file must be imported by all project files at the top of the project file. -->
    <Project ToolsVersion="4.0"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
    <VCTargetsPath>$(DepotRoot)MSBuild\Microsoft.Cpp\v4.0\v110\</VCTargetsPath>
    <VCTargetsPath11>$(DepotRoot)MSBuild\Microsoft.Cpp\v4.0\v110\</VCTargetsPath11>
    <MSBuildExtensionsPath>$(DepotRoot)MSBuild</MSBuildExtensionsPath>
    <MSBuildExtensionsPath32>$(DepotRoot)MSBuild</MSBuildExtensionsPath32>
    <VCInstallDir_110>$(DepotRoot)Microsoft Visual Studio 11.0\VC\</VCInstallDir_110>
    <VCInstallDir>$(VCInstallDir_110)</VCInstallDir>
    <WindowsKitRoot>$(DepotRoot)Windows Kits\</WindowsKitRoot>
    <WindowsSDK80Path>$(WindowsKitRoot)</WindowsSDK80Path>
    <WindowsSdkDir_80>$(WindowsKitRoot)8.0\</WindowsSdkDir_80>
    <WindowsSdkDir>$(WindowsSDKDir_80)</WindowsSdkDir>
    <WindowsSdkDir_80A>$(DepotRoot)Microsoft SDKs\Windows\v8.0A\</WindowsSdkDir_80A>
    </PropertyGroup>
    </Project>
    ```

5. 在每个项目文件中，在顶部的 `<Project Default Targets…>` 行后添加以下行。

    ```
    <Import Project="$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), Partner.AutoImports.props))\Partner.AutoImports.props"/>
    ```

6. 更改命令行环境，如下所示：

    - 设置 Depot=*在第 1 步中创建的 Depot 目录的位置*

    - 设置 path=%path%;*计算机上的 MSBuild 位置*;%Depot%\Windows\System32;%Depot%\Windows\SysWOW64;%Depot%\Microsoft Visual Studio 11.0\Common7\IDE\

         对于本机 64 位生成，请指向 64 位 MSBuild。

## <a name="see-also"></a>另请参阅
 [准备用于运行调试可执行](/cpp/windows/preparing-a-test-machine-to-run-a-debug-executable)[命令行引用](../msbuild/msbuild-command-line-reference.md)的测试计算机
