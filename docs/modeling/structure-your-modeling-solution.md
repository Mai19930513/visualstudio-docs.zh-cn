---
title: 安排你的建模解决方案
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cc4eba7dc4d185cbd8eb4f1b073fce8b0c9fb07e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85545036"
---
# <a name="structure-your-modeling-solution"></a>安排你的建模解决方案

若要在开发项目中有效地使用模型，团队成员必须能够同时在项目的不同部分的模型上工作。 本主题建议了一种将应用程序划分为对应整体分层关系图中层的不同部分的方案。

若要快速启动一个项目或子项目，使项目模板遵循你选择的项目结构非常有用。 本主题描述如何创建和使用此类模板。

本主题假定你正在处理一个大项目，这个项目大到需要多名团队成员，还可能有多个团队。 项目的代码和模型存储在源代码管理系统，例如 [!INCLUDE[esprtfs](../code-quality/includes/esprtfs_md.md)]。 至少某些团队成员使用 Visual Studio 来开发模型，其他团队成员可以通过使用其他版本的 Visual Studio 来查看模型。

若要查看支持每个工具和建模功能的 Visual Studio 版本，请参阅 [体系结构和建模工具的版本支持](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="solution-structure"></a>解决方案结构

在中型或大型项目中，团队的结构以应用程序的结构为基础。 每个团队使用一种 Visual Studio 解决方案。

### <a name="to-divide-an-application-into-layers"></a>将应用程序划分为多层

1. 将解决方案的结构建立在应用程序（例如，Web 应用程序、服务应用程序或桌面应用程序）的结构之上。 [Microsoft 应用程序体系结构指南的应用程序原型中](/previous-versions/msp-n-p/ee658107(v=pandp.10))讨论了各种常见的体系结构。

2. 创建 Visual Studio 解决方案，我们将对其进行介绍。 此解决方案将用于创建系统的整体设计。 它将包含模型但不包括代码。

   向此解决方案添加依赖关系图。 在依赖项关系图上，绘制已为应用程序选择的体系结构。 例如，关系图可能显示以下层及相互之间的依赖关系：演示、业务逻辑和数据。

4. 为体系结构依赖关系图中的每个层创建一个单独的 Visual Studio 解决方案。

   这些解决方案将用于开发层代码。

5. 创建表示层设计和所有层通用概念的模型。 排列模型，以便可以从体系结构解决方案中看到所有模型，并从各个层中看到相关模型。

   通过使用以下任一过程来实现此目的。 第一种替代方法将为每一层创建一个单独的建模项目，第二种替代方法将创建单个可在各层之间共享的建模项目。

#### <a name="use-a-separate-modeling-project-for-each-layer"></a>为每个层使用单独的建模项目

1. 为每个层解决方案创建一个建模项目。

   此模型将包含描述该层的要求和设计的关系图。 它还可以包含显示嵌套层的依赖项关系图。

   现在，每个层都有一个模型，还有一个用于应用程序体系结构的模型。 每个解决方案都包含各自的模型。 这样使团队成员能够同时在各个层上工作。

2. 对于体系结构解决方案中，将添加每个层解决方案的建模项目。 为此，请打开体系结构解决方案。 在 **解决方案资源管理器**中，右键单击解决方案节点，指向 "添加"，然后单击 " **现有项目**"。 在一个层解决方案中导航到建模项目 (.modelproj)。

   现在，每个模型都在这两个解决方案中可见：其“主”解决方案和体系结构解决方案。

3. 对于每个层的建模项目，请添加一个依赖关系图。 从体系结构依赖关系图的副本开始。 您可以删除不依赖依赖关系图的部分。

   你还可以添加表示此层的详细结构的依赖关系图。

   这些关系图用于验证在此层中开发的代码。

4. 在体系结构解决方案中，通过使用 Visual Studio 编辑所有层的要求和设计模型。

   在每个层解决方案中，引用该模型为该层开发代码。 如果你愿意将开发工作和更新模型放在不同计算机上来完成，可以使用无法创建模型的 Visual Studio 版本来阅读模型和开发代码。 你还可以在这些版本中生成模型的代码。

   此方法可保证同时编辑层模型的开发人员相互之间不会干扰。

   但是，由于各个模型是独立的，难以引用通用概念。 每个模型都必须有自己的元素副本，其他层和体系结构借助这些元素与相应模型产生依赖关系。 每一层中的依赖关系图必须与体系结构依赖关系图保持同步。 当这些元素发生更改时，很难维护同步，尽管你可以开发工具来实现这一点。

#### <a name="use-a-separate-package-for-each-layer"></a>为每个层使用单独的包

1. 在每层的解决方案中，添加体系结构建模项目。 在 **解决方案资源管理器**中，右键单击解决方案节点，指向 " **添加**"，然后单击 " **现有项目**"。 现在从每个解决方案都可以访问这个单一建模项目：体系结构项目以及每层的开发项目。

2. 在共享模型中，为每个层创建一个包：在 **解决方案资源管理器**中，选择建模项目。 在 " **UML 模型资源管理器**" 中，右键单击 "模型" 根节点，指向 " **添加**"，然后单击 " **包**"。

   每个包都包含描述相应层的要求和设计的关系图。

3. 如果需要，请为每个层的内部结构添加本地依赖关系图。

   此方法允许每层的设计元素直接引用其依赖的各个层和公共体系结构的设计元素。

   尽管对不同包的并发操作会导致一些冲突，但这些冲突非常易于管理，因为包存储在单独的文件中。

## <a name="create-architecture-templates"></a>创建体系结构模板

在实践中，您不会同时创建所有 Visual Studio 解决方案，而是在项目进展时添加它们。 你可能还会在将来的项目中使用相同的解决方案结构。 为了帮助你快速创建新的解决方案，你可以创建一个解决方案或项目模板。 可以以 Visual Studio 集成扩展 (VSIX) 格式捕捉模板，以便能够轻松地在其他计算机上分发和安装。

例如，如果你频繁使用具有演示文稿、业务和数据层的解决方案，则可以配置一个模板来创建具有这种结构的新解决方案。

### <a name="to-create-a-solution-template"></a>创建解决方案模板

1. [下载并安装 "导出模板向导"](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.ExportTemplateWizard)。

2. 创建你想要用作将来项目的起始点的解决方案结构。

3. 在“文件” **** 菜单上，单击“将模板导出为 VSIX” ****。

   将打开 "将 **模板导出为 VSIX" 向导** 。

4. 按照该向导中的说明，选择你想要包括在模板中的项目，提供模板的名称和说明，并指定输出位置。

## <a name="watch-a-video"></a>观看视频

[组织和管理模型](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-9-organizing-and-managing-your-models)

## <a name="see-also"></a>另请参阅

- [在你的开发过程中使用模型](../modeling/use-models-in-your-development-process.md)
- [Visual Studio 体系结构工具指南](../modeling/visual-studio-architecture-tooling-guidance.md)
