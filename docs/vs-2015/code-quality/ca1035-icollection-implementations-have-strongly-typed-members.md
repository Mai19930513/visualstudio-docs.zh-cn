---
title: CA1035： ICollection 实现具有强类型成员 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ICollectionImplementationsHaveStronglyTypedMembers
- CA1035
helpviewer_keywords:
- CA1035
- ICollectionImplementationsHaveStronglyTypedMembers
ms.assetid: ad404eb5-cf6a-44b7-b78a-8ebfb654bc7f
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 2e679fb3cc62ba80cfb7b56dfd7fa6590375565e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546609"
---
# <a name="ca1035-icollection-implementations-have-strongly-typed-members"></a>CA1035:ICollection 实现含有强类型成员
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|ICollectionImplementationsHaveStronglyTypedMembers|
|CheckId|CA1035|
|类别|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护类型实现 <xref:System.Collections.ICollection?displayProperty=fullName> ，但没有为提供强类型化方法 <xref:System.Collections.ICollection.CopyTo%2A?displayProperty=fullName> 。 的强类型版本 <xref:System.Collections.ICollection.CopyTo%2A> 必须接受两个参数，并且不能将 <xref:System.Array?displayProperty=fullName> 或数组 <xref:System.Object?displayProperty=fullName> 作为其第一个参数。

## <a name="rule-description"></a>规则描述
 此规则要求 <xref:System.Collections.ICollection> 实现提供强类型成员，使用户在使用该接口提供的功能时无需将参数转换为 <xref:System.Object> 类型。 此规则假定实现的类型执行此 <xref:System.Collections.ICollection> 操作是为了管理比更强的类型的实例集合 <xref:System.Object> 。

 <xref:System.Collections.ICollection> 实现 <xref:System.Collections.IEnumerable?displayProperty=fullName> 接口。 如果集合中的对象已扩展 <xref:System.ValueType?displayProperty=fullName> ，则必须为提供强类型成员， <xref:System.Collections.IEnumerable.GetEnumerator%2A> 以避免由装箱导致的性能降低。 当集合的对象为引用类型时，这不是必需的。

 若要实现接口成员的强类型版本，请使用形式的名称（例如）显式实现接口成员 `InterfaceName.InterfaceMemberName` <xref:System.Collections.ICollection.CopyTo%2A> 。 显式接口成员使用接口声明的数据类型。 使用接口成员名称（如）实现强类型成员 <xref:System.Collections.ICollection.CopyTo%2A> 。 将强类型成员声明为公共成员，并将参数和返回值声明为集合管理的强类型。 强类型取代 <xref:System.Object> 了接口所声明的更弱类型，如和 <xref:System.Array> 。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请显式实现接口成员 (将其声明为 <xref:System.Collections.ICollection.CopyTo%2A>) 。 添加已声明为的 public 强类型成员， `CopyTo` 并使其采用强类型化数组作为其第一个参数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果实现新的基于对象的集合（如二进制树，其中扩展新集合的类型确定强类型），则禁止显示此规则发出的警告。 这些类型应符合此规则并公开强类型成员。

## <a name="example"></a>示例
 下面的示例演示了实现的正确方法 <xref:System.Collections.ICollection> 。

 [!code-csharp[FxCop.Design.ICollectionStrongTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ICollectionStrongTypes/cs/FxCop.Design.ICollectionStrongTypes.cs#1)]

## <a name="related-rules"></a>相关规则
 [CA1038:枚举数应强类型化](../code-quality/ca1038-enumerators-should-be-strongly-typed.md)

 [CA1039:列表已强类型化](../code-quality/ca1039-lists-are-strongly-typed.md)

## <a name="see-also"></a>另请参阅
 <xref:System.Array?displayProperty=fullName> <xref:System.Collections.IEnumerable?displayProperty=fullName>
 <xref:System.Collections.ICollection?displayProperty=fullName>
 <xref:System.Object?displayProperty=fullName>
