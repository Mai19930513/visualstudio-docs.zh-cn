---
title: IDiaEnumTables::Skip | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::Skip method
ms.assetid: 5c9db956-0654-4f1a-8775-530aa980d8ec
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4498789b3497ea70faf9948fcf0d03c6196f250e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68161460"
---
# <a name="idiaenumtablesskip"></a>IDiaEnumTables::Skip
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

跳过枚举序列中指定数量的表。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Skip (   
   ULONG celt  
);  
```  
  
#### <a name="parameters"></a>参数  
 `celt`  
 中要跳过的枚举序列中的表数。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK` ; 否则， `S_FALSE` 如果没有其他要跳过的表，则返回。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
