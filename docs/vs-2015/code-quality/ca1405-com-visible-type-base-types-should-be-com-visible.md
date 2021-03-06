---
title: CA1405： COM 可见类型的基类型应对 COM 可见 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1405
- ComVisibleTypeBaseTypesShouldBeComVisible
helpviewer_keywords:
- CA1405
- ComVisibleTypeBaseTypesShouldBeComVisible
ms.assetid: a762ea2f-5285-4f73-bfb9-9eb10aea4290
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 779d3ec1ed520d5d48043f90e7cb6272553012a6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85535039"
---
# <a name="ca1405-com-visible-type-base-types-should-be-com-visible"></a>CA1405:COM 可见类型的基类型应对 COM 可见
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|ComVisibleTypeBaseTypesShouldBeComVisible|
|CheckId|CA1405|
|类别|Microsoft. 互操作性|
|是否重大更改|DependsOnFix|

## <a name="cause"></a>原因
 组件对象模型 (COM) 可见类型派生自非 COM 可见的类型。

## <a name="rule-description"></a>规则描述
 当 COM 可见类型在新版本中添加成员时，必须遵守严格指导原则，以避免中断绑定到当前版本的 COM 客户端。 对于 COM 不可见的类型，假设在添加新成员时，不需要遵循这些 COM 版本控制规则。 但是，如果 COM 可见类型派生自 COM 不可见类型，并公开了 <xref:System.Runtime.InteropServices.ClassInterfaceType?displayProperty=fullName> 或 <xref:System.Runtime.InteropServices.ClassInterfaceType> (默认) 的类接口，则基类型的所有公共成员将 (，除非它们特别标记为 com 不可见，这将是向 com 公开的冗余) 。 如果基类型在后续版本中添加了新成员，则绑定到派生类型的类接口的任何 COM 客户端都可能会中断。 COM 可见类型应仅从 COM 可见类型派生，以减少中断 COM 客户端的可能性。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请使基类型 COM 可见或派生类型 COM 不可见。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示违反规则的类型。

 [!code-csharp[FxCop.Interoperability.ComBaseTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComBaseTypes/cs/FxCop.Interoperability.ComBaseTypes.cs#1)]
 [!code-vb[FxCop.Interoperability.ComBaseTypes#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComBaseTypes/vb/FxCop.Interoperability.ComBaseTypes.vb#1)]

## <a name="see-also"></a>另请参阅
 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute?displayProperty=fullName>[类接口简介](https://msdn.microsoft.com/733c0dd2-12e5-46e6-8de1-39d5b25df024)[与非托管代码互](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)操作
