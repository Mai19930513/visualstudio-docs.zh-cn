---
title: IDebugComPlusSymbolProvider：： UnloadSymbols |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- UnloadSymbols
- IDebugComPlusSymbolProvider::UnloadSymbols
ms.assetid: 53e3ddc1-ab47-4097-8fef-b26e5504b37a
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ad78f1b569180a93b195f6a4076cc7396dcf8e53
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68176782"
---
# <a name="idebugcomplussymbolproviderunloadsymbols"></a>IDebugComPlusSymbolProvider::UnloadSymbols
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

从内存中卸载指定模块的调试符号。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT UnloadSymbols(  
   ULONG32 ulAppDomainID,  
   GUID    guidModule  
);  
```  
  
```csharp  
int UnloadSymbols(  
   uint ulAppDomainID,  
   Guid guidModule  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ulAppDomainID`  
 中应用程序域的标识符。  
  
 `guidModule`  
 中模块的唯一标识符。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="example"></a>示例  
 下面的示例演示如何为公开[IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)接口的**CDebugSymbolProvider**对象实现此方法。  
  
```cpp#  
HRESULT CDebugSymbolProvider::UnloadSymbols(  
    ULONG32 ulAppDomainID,  
    GUID guidModule  
)  
{  
    HRESULT hr = S_OK;  
    CComPtr<CModule> pmodule;  
    Module_ID idModule(ulAppDomainID, guidModule);  
  
    METHOD_ENTRY( CDebugSymbolProvider::UnloadSymbols );  
  
#if DEBUG  
  
    DebugVerifyModules();  
#endif  
  
    IfFailGo( GetModule( idModule, &pmodule ) );  
  
#if DEBUG  
  
    DebugVerifyModules();  
#endif  
  
    RemoveModule( pmodule );  
    pmodule->Cleanup();  
  
Error:  
#if DEBUG  
  
    DebugVerifyModules();  
#endif  
  
    METHOD_EXIT( CDebugSymbolProvider::UnloadSymbols, hr );  
  
    return hr;  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
