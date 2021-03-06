---
title: 正在为并行部署注册文件扩展名 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- file extensions, registering for side-by-side
ms.assetid: 9ab046a2-147d-4167-aa14-7d661b1eaaa5
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 354b91dd1282df9726c1ee9c47f610b0dfdd9c1a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68163701"
---
# <a name="registering-file-name-extensions-for-side-by-side-deployments"></a>注册并行部署的文件扩展名
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

对于在并行环境中部署的 Vspackage，必须注册文件扩展名，以便将文件与正确版本的相关联 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。 如果你使用特定于版本的文件扩展名，则注册使用户能够在适当版本的中打开你的项目和项目项文件 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。  
  
## <a name="in-this-section"></a>本节内容  
 [关于文件扩展名](../extensibility/about-file-name-extensions.md)  
 讨论文件扩展名的注册方式。  
  
 [指定文件扩展名的文件处理程序](../extensibility/specifying-file-handlers-for-file-name-extensions.md)  
 提供有关如何注册可打开、编辑等特定文件扩展名的应用程序的信息。  
  
 [注册文件扩展名的谓词](../extensibility/registering-verbs-for-file-name-extensions.md)  
 讨论如何注册谓词。  
  
 [管理并行文件关联](../extensibility/managing-side-by-side-file-associations.md)  
 讨论如何处理并行安装，其中应调用的特定版本 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 来打开文件。  
  
## <a name="related-sections"></a>相关章节  
 [支持多个版本的 Visual Studio](../extensibility/supporting-multiple-versions-of-visual-studio.md)  
 在开发和向最终用户部署的过程中，描述与多个版本的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 和你的 VSPackage 相关的问题。
