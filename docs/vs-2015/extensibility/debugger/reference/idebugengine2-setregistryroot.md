---
title: IDebugEngine2：： SetRegistryRoot |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEngine2::SetRegistryRoot
helpviewer_keywords:
- IDebugEngine2::SetRegistryRoot
ms.assetid: d0d81202-8a4a-4bc3-b297-30a047c5ec60
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 39bb532301d34a3abf9988cfa909e1606c3c73e8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68195948"
---
# <a name="idebugengine2setregistryroot"></a>IDebugEngine2::SetRegistryRoot
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

设置调试引擎的注册表根 (DE) 。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT SetRegistryRoot(   
   LPCOLESTR pszRegistryRoot  
);  
```  
  
```csharp  
int SetRegistryRoot(   
   string pszRegistryRoot  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pszRegistryRoot`  
 中要使用的注册表根目录。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法允许 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 指定应使用的备用注册表根以获取注册表设置，例如 "HKEY_LOCAL_MACHINE \software\microsoft\visualstudio\8.0exp"。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
