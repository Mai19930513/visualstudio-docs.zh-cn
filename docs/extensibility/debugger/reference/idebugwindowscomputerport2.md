---
title: IDebugWindowsComputerPort2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugWindowsComputerPort2 interface
ms.assetid: 25f327b8-0303-4268-88d1-74df630436aa
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9ef4162469651e4b69502d3a9639d1e86c62e0b7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80718224"
---
# <a name="idebugwindowscomputerport2"></a>IDebugWindowsComputerPort2
允许查询有关目标计算机的信息。

## <a name="syntax"></a>语法

```
IDebugWindowsComputerPort2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 此接口由会话调试管理器的端口对象实现。

## <a name="methods"></a>方法
 下表显示的方法 `IDebugWindowsComputerPort2` 。

|方法|说明|
|------------|-----------------|
|[GetComputerInfo](../../../extensibility/debugger/reference/idebugwindowscomputerport2-getcomputerinfo.md)|检索有关正在运行调试器的计算机的信息。|

## <a name="requirements"></a>要求
 标头： Msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
