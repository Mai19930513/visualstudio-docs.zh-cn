---
title: IDebugProcess2：： EnumPrograms |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProcess2::EnumPrograms
helpviewer_keywords:
- IDebugProcess2::EnumPrograms
ms.assetid: f5b7295d-487d-464f-a4c6-d54175b07705
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8391bdd01d33a39810ed45f56cd064e76464153e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68188032"
---
# <a name="idebugprocess2enumprograms"></a>IDebugProcess2::EnumPrograms
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

检索此进程包含的所有程序的列表。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT EnumPrograms(   
   IEnumDebugPrograms2** ppEnum  
);  
```  
  
```csharp  
int EnumPrograms(   
   out IEnumDebugPrograms2 ppEnum  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppEnum`  
 弄返回一个 [IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md) 对象，该对象包含进程中的所有程序的列表。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)   
 [IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md)
