---
title: 通过 Python 入门 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-python
ms.topic: conceptual
ms.assetid: 33f4f6fb-0ae4-4234-9df2-531f2d3af17f
caps.latest.revision: 13
author: kraigb
ms.author: kraigb
manager: jillfra
ms.openlocfilehash: 97d60fe31f838c4cc497701f4560dc426ebc1cc9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80543978"
---
# <a name="getting-started-with-python"></a>Python 入门
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

针对 Visual Studio 的 Python 工具 (PTVS) 是一个适用于 Visual Studio 的免费 [开源](https://github.com/Microsoft/ptvs) 插件，它具有强大的 Python 开发体验。  
  
## <a name="python-the-language"></a>Python 语言
  
Python 是一种常用的编程语言，由许多大学、科学家、应用程序脚本、随意开发人员和专业开发人员使用，可处理应用程序、网站和云服务。

作为编程语言，Python 是：
  
- 可靠。
- 通常适用于编写快速程序、应用脚本、桌面应用、web 服务器、web 服务和科学计算。
- 易于学习，设计良好，能帮助提高编码质量（许多大学都将它用于编程入门课程）。
- 灵活，支持强制性、功能和面向对象的编程样式。
- 免费且开源。
- 在所有主要的操作系统上正常运行。  
- 受许多免费、有用且设计良好的库支持。  
- 由大量文档、示例和强大的开发人员社区支持。  

若要了解有关该语言的详细信息，请从用于 python.org 的 [初学者着手 Python](https://www.python.org/about/gettingstarted/) 。

若要安装 Python，请访问 [https://www.python.org/download/](https://www.python.org/download/) 。

## <a name="python-tools-for-visual-studio"></a>Python Tools for Visual Studio
  
针对 Visual Studio 的 Python 工具（可从 [visualstudio.com](https://www.visualstudio.com/explore/python-vs)安装）提供以下功能：  
  
- 支持多种解释器：各种版本的 CPython、IronPython 以及 IPython  
- 项目系统可隐式选取 Python 代码的文件夹结构，也允许显式控制，以便标识应用代码、测试代码、网页、JavaScript、生成脚本等等。  
- 用于控制台、Web、Azure、数据科学和其他类型项目的项目模板。    
- Azure SDK for Python (参见下面的)     
- 丰富的编辑和代码理解功能，包括语法着色、跨所有代码和库的自动完成功能、签名帮助、类视图、转到定义、查找所有引用、重构等等。    
- 交互式 (REPL) 窗口
- 使用数据可视化功能的 IPython。
- 支持 IronPython 和 .NET/WPF。    
- 丰富的无需 Visual Studio 项目的调试功能，包括可对现有可执行文件进行调试、混合模式调试、对 Windows/Linux/Mac 进行远程调试，以及在交互式窗口中进行调试。   
- 分析工具。  
- 测试工具。  
  
下列资源可帮你入门：

- [安装指南](https://github.com/Microsoft/PTVS/wiki/PTVS-Installation)    
- [入门和深入了解短片](https://www.youtube.com/playlist?list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)  
- 安装和功能演示 (27 分钟) ] (https://www.youtube.com/watch?v=JNNAOypc6Ek)  
- [文档](https://github.com/Microsoft/PTVS/wiki)  

请注意，Visual Studio 目前不提供使用 Python 创建独立可执行文件的方法，这实质上是指具有嵌入的 Python 解释器的程序。 但是，如 [StackOverflow](https://stackoverflow.com/questions/5458048/how-to-make-a-python-script-standalone-executable-to-run-without-any-dependency) 所述，Python 社区中有多种方法可以实现此功能。 CPython 还支持嵌入到本机应用程序中，如博客文章中所述， [使用 CPython 的可嵌入 Zip 文件](https://devblogs.microsoft.com/python/cpython-embeddable-zip-file/)。
  
## <a name="building-ui-with-python"></a>通过 Python 生成 UI  

使用 Python 生成 UI 的主要产品是[Qt 项目](https://www.qt.io/qt-for-application-development/)，其中包含 python 的绑定（称为 PySide） [ (官方绑定) ](https://wiki.qt.io/PySide) (还请参阅 PySide 和[PyQt](https://wiki.python.org/moin/PyQt)) [下载](https://download.qt.io/official_releases/pyside/.)。 目前，Visual Studio 中的 Python 支持不包括用于 UI 开发的任何特定工具。

## <a name="azure-sdk-for-python"></a>用于 Python 的 Azure SDK
  
Azure SDK for Python 支持 Windows、Mac 和 Linux，使得使用和管理 Microsoft Azure 服务更加方便。 请参阅下列资源了解详细信息： 

- 若要安装 SDK，请使用 [Python 软件包索引](https://pypi.python.org/pypi/azure)或者按照 Azure 文档中的[安装 Python 和 SDK](/azure/developer/python/azure-sdk-install) 的说明进行操作。 
- [Azure SDK for Python 开发人员中心](https://azure.microsoft.com/develop/python/)通过教程提供许多从安装到文档的帮助。  以下为一些要点：  
- 操作指南：
  - [存储 Blob](https://azure.microsoft.com/develop/python/how-to-guides/blob-service/)  
  - [存储队列](https://azure.microsoft.com/develop/python/how-to-guides/queue-service/)  
  - [存储表](https://azure.microsoft.com/develop/python/how-to-guides/table-service/)  
  - [服务总线队列](https://azure.microsoft.com/develop/python/how-to-guides/service-bus-queues/)
  - [服务总线主题/订阅](https://azure.microsoft.com/develop/python/how-to-guides/service-bus-topics/) 
  - [服务管理](https://azure.microsoft.com/develop/python/how-to-guides/service-management/)  

## <a name="scientific-computing"></a>科学计算

除所有 Python 数据科学家库以外，Python Tools for Visual Studio 也支持 IPython 和 IPython 笔记本（可以在 Azure 中托管）。

我们建议从[加利福尼亚大学欧文分校](https://www.lfd.uci.edu/~gohlke/pythonlibs/#scipy-stack)获取 IPython 和科学计算库（matplotlib、scipy、numpy 等）。  
  
## <a name="see-also"></a>另请参阅  

[入门与 PTVS：设置 Visual Studio](../python/getting-started-with-ptvs-setting-up-visual-studio.md) 
[入门与 PTVS：开始编码 (项目) ](../python/getting-started-with-ptvs-start-coding-projects.md) 
[入门与 PTVS：编辑代码](../python/getting-started-with-ptvs-editing-code.md) 
[入门与 PTVS：调试](../python/getting-started-with-ptvs-debugging.md) 
[入门与 PTVS： Interactive Python](../python/getting-started-with-ptvs-interactive-python.md) 
[使用 PTVS 入门：在 Azure 中构建网站](../python/getting-started-with-ptvs-building-a-website-in-azure.md)
