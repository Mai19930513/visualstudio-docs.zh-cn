---
title: CA1821：删除空终结器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- RemoveEmptyFinalizers
- CA1821
helpviewer_keywords:
- CA1821
ms.assetid: 3f4855a0-e4a0-46e6-923c-4c3b7074048d
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a2e704202773447e353f041df66b05cb5f648c00
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85545348"
---
# <a name="ca1821-remove-empty-finalizers"></a>CA1821:移除空终结器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|RemoveEmptyFinalizers|
|CheckId|CA1821|
|类别|Microsoft. 性能|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 类型实现了一个空的终结器，只调用基类型的终结器或只调用有条件发出的方法。

## <a name="rule-description"></a>规则描述
 应尽可能避免终结器，因为跟踪对象生存期会产生额外的性能系统开销。 垃圾回收器将在收集对象之前运行终结器。 这意味着将需要两个集合来收集对象。 空终结器会产生这种额外的开销，而不会带来任何好处。

## <a name="how-to-fix-violations"></a>如何解决冲突
 删除空的终结器。 如果调试需要终结器，请将整个终结器置于 `#if DEBUG / #endif` 指令中。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 请勿禁止显示此规则的消息。 取消终止失败会降低性能，而不会带来任何好处。

## <a name="example"></a>示例
 下面的示例演示了应删除的空终结器、应括在指令中的终结器 `#if DEBUG / #endif` 以及正确使用指令的终结器 `#if DEBUG / #endif` 。

 [!code-csharp[FxCop.Performance.RemoveEmptyFinalizers#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.RemoveEmptyFinalizers/cs/FxCop.Performance.RemoveEmptyFinalizers.cs#1)]
