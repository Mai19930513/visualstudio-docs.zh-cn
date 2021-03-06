---
title: ReceiveAndSendReply 模板设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.ReceiveAndSendReply.UI
- System.ServiceModel.Activities.SendReply.UI
ms.assetid: d1d9a058-df7e-48f5-a2e7-3caeeba7eaa6
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4c00eed244867cfd38b20f6a8f065fc6da006801
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80395391"
---
# <a name="receiveandsendreply-template-designer"></a>ReceiveAndSendReply 模板设计器
**ReceiveAndSendReply**模板用于在活动中创建一对预配置的 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.SendReply> 活动，这些活动与 <xref:System.Activities.Statements.Sequence> 服务器上的请求/响应消息交换模式的一部分相关。

## <a name="the-receiveandsendreply-template"></a>ReceiveAndSendReply 模板
 添加 **ReceiveAndSendReply** 模板除了 <xref:System.ServiceModel.Activities.Receive> 使用活动创建和活动之外，还执行三个操作 <xref:System.ServiceModel.Activities.SendReply> <xref:System.Activities.Statements.Sequence> ：

1. 配置 <xref:System.ServiceModel.Activities.Receive.OperationName%2A> 活动的 <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A> 和 <xref:System.ServiceModel.Activities.Receive> 属性。

2. 将 <xref:System.ServiceModel.Activities.SendReply.Request%2A> 活动的 <xref:System.ServiceModel.Activities.Receive> 属性绑定到 <xref:System.ServiceModel.Activities.Send> 活动。

3. 创建一个 <xref:System.ServiceModel.Activities.CorrelationHandle> 作为父活动中的一个变量。

### <a name="using-the-receiveandsendreply-template-designer"></a>使用 ReceiveAndSendReply 模板设计器
 " **ReceiveAndSendReply** " 活动设计器可在 "**工具箱**" 的 "**消息传送**" 类别中找到，可通过单击 (中的 "**工具箱**" 选项卡进行访问 [!INCLUDE[wfd2](../includes/wfd2-md.md)] ，也可以从 "**视图**" 菜单中选择 "**工具栏**" 或按 CTRL + ALT + X。 ) 

 可以将 " **ReceiveAndSendReply** " 活动设计器从 " **工具箱** " 拖放到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上通常放置活动的任何位置。 这会创建一个 <xref:System.ServiceModel.Activities.Receive> 活动，该活动可使用 " **发送** 活动设计器" 和一个 <xref:System.ServiceModel.Activities.SendReply> 可使用 SendReplyToReceive 设计器进行配置的相关配置。

 [!INCLUDE[crabout](../includes/crabout-md.md)] 使用 **接收** 设计器配置 <xref:System.ServiceModel.Activities.Receive> 活动，请参阅 [接收](../workflow-designer/receive-activity-designer.md) 主题。

 [!INCLUDE[crabout](../includes/crabout-md.md)] 使用 **SendReplyToReceive** 设计器配置 <xref:System.ServiceModel.Activities.SendReply> 活动，请参阅下一节。

### <a name="properties-of-sendreply"></a>SendReply 的属性
 下表列出 <xref:System.ServiceModel.Activities.SendReply> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中进行编辑，其中一些属性还可以在 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 设计器图面上进行编辑。

|                               属性名称                                | 必选 |                                                                                                                                                                                                                                                                                                                                                      使用情况                                                                                                                                                                                                                                                                                                                                                       |
|----------------------------------------------------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              <xref:System.Activities.Activity.DisplayName%2A>              |  错误   |                                                                                                                                                                                            <xref:System.ServiceModel.Activities.SendReply> 活动的可选友好名称。 默认值为 SendReplyToReceive。<br /><br /> 虽然对友好 <xref:System.Activities.Activity.DisplayName%2A> 使用非默认值不是绝对必需的，但最好使用非默认值。                                                                                                                                                                                             |
|         <xref:System.ServiceModel.Activities.SendReply.Request%2A>         |   正确   | 对与此 <xref:System.ServiceModel.Activities.Receive> 活动配对的 <xref:System.ServiceModel.Activities.SendReply> 活动的引用。 此属性不能为 **null**。 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.SendReply> 活动在服务器上一起使用，以对请求/响应消息模式进行建模。 此属性指定配对的 <xref:System.ServiceModel.Activities.Send> 活动。 在该设计器中无法编辑此属性，因为它自动绑定到从中创建了 <xref:System.ServiceModel.Activities.Send> 活动的 <xref:System.ServiceModel.Activities.SendReply> 活动。 |
|         <xref:System.ServiceModel.Activities.SendReply.Content%2A>         |  错误   |                       指定要接收的消息或参数内容。 它可为 <xref:System.ServiceModel.Activities.ReceiveMessageContent> 活动或 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 活动。 编辑此属性，方法是单击属性网格中 "**内容**" 字段旁边的省略号按钮，或单击 "**定义 ...** " "**接收**" 活动设计器图面上的 "**内容**" 标签旁边的按钮。 两者都显示 " **内容定义** " 对话框。 [!INCLUDE[crabout](../includes/crabout-md.md)] 如何使用此框，请参阅 " [内容定义" 对话框](../workflow-designer/content-definition-dialog-box.md) 主题。                       |
| <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> |  错误   |            指定在工作流中对配置此 <xref:System.ServiceModel.Activities.CorrelationInitializer> 活动的多个 <xref:System.ServiceModel.Activities.CorrelationHandle> 对象进行初始化的 <xref:System.ServiceModel.Activities.Receive> 对象的集合。 在 "属性" 网格中单击属性旁的省略号按钮， <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> 以打开 " **添加相关初始值设定项** " 对话框。 [!INCLUDE[crabout](../includes/crabout-md.md)] 使用此框，请参阅 " [添加 CorrelationInitializers" 对话框](../workflow-designer/add-correlationinitializers-dialog-box.md) 主题。            |
|         <xref:System.ServiceModel.Activities.SendReply.Action%2A>          |  错误   |                                                                                                                                                                                                                                              指定消息的操作标头。 如果未显式设置，则它的默认值为：<br /><br /> `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}`                                                                                                                                                                                                                                              |
|    <xref:System.ServiceModel.Activities.SendReply.PersistBeforeSend%2A>    |  错误   |                                                                                                                                                                                                                                                                                          指定在发送回复消息前是否应保留工作流实例。 默认值是 **false**秒。                                                                                                                                                                                                                                                                                           |

## <a name="see-also"></a>另请参阅
 [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md) [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md) [Receive](../workflow-designer/receive-activity-designer.md) [Send](../workflow-designer/send-activity-designer.md) [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md) [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)