---
title: CA1019：定义特性参数的访问器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1019
- DefineAccessorsForAttributeArguments
helpviewer_keywords:
- CA1019
- DefineAccessorsForAttributeArguments
ms.assetid: 197f2378-3c43-427e-80de-9ec25006c05c
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ec9be9dae502ec48570a85576f483518ed0d75d6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85534948"
---
# <a name="ca1019-define-accessors-for-attribute-arguments"></a>CA1019:定义特性参数的访问器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|DefineAccessorsForAttributeArguments|
|CheckId|CA1019|
|类别|Microsoft. Design|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 在其构造函数中，属性定义了不具有相应属性的参数。

## <a name="rule-description"></a>规则描述
 特性可以定义强制自变量，在对目标应用该特性时必须指定这些自变量。 这些实参也称为位置实参，因为它们将作为位置形参提供给特性构造函数。 对于每一个强制变量，特性还必须提供一个相应的只读属性，以便可以在执行时检索该变量的值。 此规则检查是否为每个构造函数参数定义了相应的属性。

 特性还可以定义可选实参，可选实参也称为命名实参。 这些变量按名称提供给特性构造函数，并且必须具有相应的读/写属性。

 对于必需参数和可选参数，对应的属性和构造函数参数应该使用相同的名称，但大小写不同。 属性使用 Pascal 大小写，参数使用 camel 大小写。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请为每个没有的构造函数参数添加一个只读属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果你不希望可检索必需参数的值，则禁止显示此规则发出的警告。

## <a name="custom-attributes-example"></a>自定义特性示例

### <a name="description"></a>说明
 下面的示例演示两个定义 (位置) 参数的属性。 未正确定义属性的第一个实现。 第二种实现是正确的。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Design.AttributeAccessors#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeAccessors/cs/FxCop.Design.AttributeAccessors.cs#1)]
 [!code-vb[FxCop.Design.AttributeAccessors#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeAccessors/vb/FxCop.Design.AttributeAccessors.vb#1)]

## <a name="positional-and-named-arguments"></a>位置和命名参数

### <a name="description"></a>说明
 位置和命名参数使库的使用者清楚哪些参数对于属性是必需的，哪些参数是可选的。

 下面的示例演示具有位置和命名参数的属性的实现。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Design.AttributeAccessorsNamed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeAccessorsNamed/cs/FxCop.Design.AttributeAccessorsNamed.cs#1)]

### <a name="comments"></a>注释
 下面的示例演示如何将自定义属性应用于两个属性。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Design.AttributeAccessorsNamedApplied#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeAccessorsNamedApplied/cs/FxCop.Design.AttributeAccessorsNamedApplied.cs#1)]

## <a name="related-rules"></a>相关规则
 [CA1813:避免使用非密封特性](../code-quality/ca1813-avoid-unsealed-attributes.md)

## <a name="see-also"></a>另请参阅
 [特性](https://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b)
