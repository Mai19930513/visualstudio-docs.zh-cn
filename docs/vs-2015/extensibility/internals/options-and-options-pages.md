---
title: 选项和选项页 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], managed package framework support
- managed package framework, Tools Options pages support
- support, Tools Options pages
- Tools Options pages [Visual Studio SDK], layouts
- Tools Options pages [Visual Studio SDK], attributes
ms.assetid: e6c0e636-5ec3-450e-b395-fc4bb9d75918
caps.latest.revision: 35
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4512867f636e2362aa28d52c5af28bf8eb9697f9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "75851153"
---
# <a name="options-and-options-pages"></a>选项和选项页
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

单击 "**工具**" 菜单上的 "**选项**" 将打开 "**选项**" 对话框。 此对话框中的选项统称为 "选项页"。 导航窗格中的树控件包含选项类别，每个类别都包含 "选项" 页。 选择某个页面后，其选项将显示在右窗格中。 这些页面使你可以更改用于确定 VSPackage 状态的选项的值。  
  
## <a name="support-for-options-pages"></a>支持选项页  
 <xref:Microsoft.VisualStudio.Shell.Package>类支持创建选项页和选项类别。 <xref:Microsoft.VisualStudio.Shell.DialogPage>类实现选项页。  
  
 的默认实现 <xref:Microsoft.VisualStudio.Shell.DialogPage> 向用户提供其公共属性。 您可以通过重写页面上的各种方法来自定义此行为，以创建具有其自己的用户界面 (UI) 的自定义选项页。 有关详细信息，请参阅 [创建选项页](../../extensibility/creating-an-options-page.md)。  
  
 <xref:Microsoft.VisualStudio.Shell.DialogPage>类实现 <xref:Microsoft.VisualStudio.Shell.IProfileManager> ，该方法为选项页提供持久性，并为用户设置提供持久性。 <xref:Microsoft.VisualStudio.Shell.IProfileManager.LoadSettingsFromStorage%2A>如果属性可以与字符串相互转换，则和方法的默认实现 <xref:Microsoft.VisualStudio.Shell.IProfileManager.SaveSettingsToStorage%2A> 会将属性更改保存到注册表的用户部分。  
  
## <a name="options-page-registry-path"></a>选项页注册表路径  
 默认情况下，由 "选项" 页管理的属性的注册表路径由 " <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A> 选项" 页类的组合、单词 dialogpage 派生和类型名称确定。 例如，可以按如下所示定义选项页类。  
  
 [!code-csharp[VSSDKSupportForOptionsPages#1](../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs#1)]
 [!code-vb[VSSDKSupportForOptionsPages#1](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb#1)]  
  
 如果 <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A> 是 HKEY_CURRENT_USER \software\microsoft\visualstudio\8.0exp，则属性名称和值对是 HKEY_CURRENT_USER \software\microsoft\visualstudio\8.0exp\dialogpage\company.optionspage.optionspagegeneral. 的子项。  
  
 "选项" 页本身的注册表路径由 " <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> 单词"、"ToolsOptionsPages" 和 "选项" 页类别和名称确定。 例如，如果 "自定义选项" 页具有 "类别"、"我的选项" 页，并且 " <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> HKEY_LOCAL_MACHINE \software\microsoft\visualstudio\8.0exp"，则 "选项" 页具有注册表项，HKEY_LOCAL_MACHINE \Software\microsoft\visualstudio\8.0exp\toolsoptionspages\my 选项 Pages\Custom。  
  
## <a name="toolsoptions-page-attributes-and-layout"></a>"工具/选项" 页属性和布局  
 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>特性确定将自定义选项页分组到 "**选项**" 对话框的导航树中的类别。 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>属性将选项页与提供接口的 VSPackage 相关联。 考虑以下代码片断：  
  
 [!code-csharp[VSSDKSupportForOptionsPages#2](../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs#2)]
 [!code-vb[VSSDKSupportForOptionsPages#2](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb#2)]  
  
 这声明 MyPackage 提供了两个选项页： OptionsPageGeneral 和 OptionsPageCustom。 在 " **选项** " 对话框中，这两个选项页在 " **我的选项页** " 类别中分别显示为 " **常规** " 和 " **自定义**"。  
  
## <a name="option-attributes-and-layout"></a>选项属性和布局  
 页面提供的用户界面 (UI) 确定自定义选项页中选项的外观。 "常规选项" 页中的选项布局、标签和说明由以下属性确定：  
  
- <xref:System.ComponentModel.CategoryAttribute> 确定选项的类别。  
  
- <xref:System.ComponentModel.DisplayNameAttribute> 确定选项的显示名称。  
  
- <xref:System.ComponentModel.DescriptionAttribute> 确定选项的说明。  
  
  > [!NOTE]
  > 等效属性、SRCategory、LocDisplayName 和 SRDescription，使用字符串资源进行本地化，并在 [托管项目示例](https://msdn.com/vsx)中定义。  
  
  考虑以下代码片断：  
  
  [!code-csharp[VSSDKSupportForOptionsPages#3](../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/optionspagecustom.cs#3)]
  [!code-vb[VSSDKSupportForOptionsPages#3](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/optionspagegeneral.vb#3)]  
  
  "选项" 页上的 "OptionInteger" 选项显示为 "**我的选项**" 类别中的**整数选项**。 如果选择了该选项，则 "说明" 框中会显示 " **我的整数" 选项**。  
  
## <a name="accessing-options-pages-from-another-vspackage"></a>访问其他 VSPackage 的选项页  
 承载和管理选项页的 VSPackage 可以通过使用自动化模型以编程方式从另一个 VSPackage 访问。 例如，在以下代码中，VSPackage 注册为承载选项页。  
  
 [!code-csharp[VSSDKSupportForOptionsPages#4](../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs#4)]
 [!code-vb[VSSDKSupportForOptionsPages#4](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb#4)]  
  
 以下代码片段从 MyOptionPage 中获取 OptionInteger 的值：  
  
 [!code-csharp[VSSDKSupportForOptionsPages#5](../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs#5)]
 [!code-vb[VSSDKSupportForOptionsPages#5](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb#5)]  
  
 当 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> 属性注册选项页时，如果该特性的参数为，则该页将在 automationproperties.livesetting 项下进行注册 `SupportsAutomation` `true` 。 自动检查此注册表项以查找关联的 VSPackage，然后通过 "托管选项" 页（在本例中为 "我的网格" 页）访问属性。  
  
 自动化属性的注册表路径由 " <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> 单词"、"automationproperties.livesetting" 和 "选项" 页类别和名称确定。 例如，如果 "选项" 页具有 "我的类别" 类别、"我的网格" 页名称和 <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> HKEY_LOCAL_MACHINE \software\microsoft\visualstudio\8.0exp，则自动化属性具有注册表项，HKEY_LOCAL_MACHINE \Software\microsoft\visualstudio\8.0exp\automationproperties\my Category\My 网格页。  
  
> [!NOTE]
> 规范名称 "我的 Category.My" 网格页是此项的 Name 子项的值。
