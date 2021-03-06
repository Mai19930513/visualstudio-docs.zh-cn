---
title: 更改菜单命令的文本 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- menus, changing text
- text, menus
- commands, changing text
ms.assetid: 5cb676a0-c6e2-47e5-bd2b-133dc8842e46
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d8fd3fc01a5dd3e10e633b876b719695d6b26c18
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184496"
---
# <a name="changing-the-text-of-a-menu-command"></a>更改菜单命令的文本
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

以下步骤演示如何使用服务更改菜单命令的文本标签 <xref:System.ComponentModel.Design.IMenuCommandService> 。  
  
## <a name="changing-a-menu-command-label-with-the-imenucommandservice"></a>使用 IMenuCommandService 更改菜单命令标签  
  
1. `MenuText`使用名为**ChangeMenuText**的菜单命令创建一个名为的 VSIX 项目。 有关详细信息，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。  
  
2. 在 vstc 文件中，将标志添加 `TextChanges` 到菜单命令中，如下面的示例中所示。  
  
    ```xml  
    <Button guid="guidChangeMenuTextPackageCmdSet" id="ChangeMenuTextId" priority="0x0100" type="Button">  
        <Parent guid="guidChangeMenuTextPackageCmdSet" id="MyMenuGroup" />  
        <Icon guid="guidImages" id="bmpPic1" />  
        <CommandFlag>TextChanges</CommandFlag>  
        <Strings>  
            <ButtonText>Invoke ChangeMenuText</ButtonText>  
        </Strings>  
    </Button>  
    ```  
  
3. 在 ChangeMenuText.cs 文件中，创建一个将在显示菜单命令之前调用的事件处理程序。  
  
    ```csharp  
    private void OnBeforeQueryStatus(object sender, EventArgs e)  
    {  
        var myCommand = sender as OleMenuCommand;  
        if (null != myCommand)  
        {  
            myCommand.Text = "New Text";  
                    }  
    }  
    ```  
  
     还可以通过更改 <xref:System.ComponentModel.Design.MenuCommand.Visible%2A> 对象的、和属性来更新此方法中的菜单命令的状态 <xref:System.ComponentModel.Design.MenuCommand.Checked%2A> <xref:System.ComponentModel.Design.MenuCommand.Enabled%2A> <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 。  
  
4. 在 ChangeMenuText 构造函数中，将原始命令初始化和位置代码替换为创建 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> (而不是 `MenuCommand` 表示菜单命令的) 的代码， <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> 并添加事件处理程序，并为菜单命令服务提供菜单命令。  
  
     如下所示：  
  
    ```csharp  
    private ChangeMenuText(Package package)  
    {  
        if (package == null)  
        {  
            throw new ArgumentNullException(nameof(package));  
        }  
  
        this.package = package;  
  
        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;  
        if (commandService != null)  
        {  
            CommandID menuCommandID = new CommandID(MenuGroup, CommandId);  
            EventHandler eventHandler = this.ShowMessageBox;  
            OleMenuCommand menuItem = new OleMenuCommand(ShowMessageBox, menuCommandID);  
            menuItem.BeforeQueryStatus +=  
                new EventHandler(OnBeforeQueryStatus);  
            commandService.AddCommand(menuItem);  
        }  
    }  
    ```  
  
5. 生成项目并启动调试。 此时将显示 Visual Studio 的实验实例。  
  
6. 在 " **工具** " 菜单中，应会看到名为 " **调用 ChangeMenuText**" 的命令。  
  
7. 单击该命令。 应该会看到消息框，指出已调用 MenuItemCallback。 关闭消息框时，应会看到 "工具" 菜单上的命令名称现在为 " **新文本**"。
