---
title: 'Idiadatasource:: Loadandvalidatedatafrompdb |Microsoft Docs'
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::loadAndValidateDataFromPdb method
ms.assetid: d66712dd-6c24-4192-919a-cce262066f0e
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4e4b425406f6f6b044226b791950f7d93acc95aa
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2018
ms.locfileid: "47480443"
---
# <a name="idiadatasourceloadandvalidatedatafrompdb"></a>IDiaDataSource::loadAndValidateDataFromPdb
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

本主题的最新版本，请参阅[idiadatasource:: Loadandvalidatedatafrompdb](https://docs.microsoft.com/visualstudio/debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb)。  
  
打开和验证程序数据库 (.pdb) 文件匹配，所提供的签名信息并准备将.pdb 文件作为调试数据源。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT loadAndValidateDataFromPdb (   
   LPCOLESTR pdbPath,  
   GUID*     pcsig70,  
   DWORD     sig,  
   DWORD     age  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pdbPath`  
 [in].Pdb 文件的路径。  
  
 `pcsig70`  
 [in]要针对.pdb 文件签名验证的 GUID 签名。 仅.pdb 文件在[!INCLUDE[vcprvc](../../includes/vcprvc-md.md)]和更高版本具有 GUID 签名。  
  
 `sig`  
 [in]要针对.pdb 文件签名验证的 32 位签名。  
  
 `age`  
 [in]若要验证的生存期值。 为任何已知的时间值不一定对应保留时间，使用它来确定.pdb 文件是否与相应的.exe 文件不同步。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。 下表显示了可能的此方法的返回值。  
  
|“值”|描述|  
|-----------|-----------------|  
|E_PDB_NOT_FOUND|无法打开该文件，或该文件具有无效的格式。|  
|E_PDB_FORMAT|尝试访问具有过时的格式的文件。|  
|E_PDB_INVALID_SIG|签名不匹配。|  
|E_PDB_INVALID_AGE|年龄不匹配。|  
|E_INVALIDARG|参数无效。|  
|E_UNEXPECTED|已准备好数据源。|  
  
## <a name="remarks"></a>备注  
 .Pdb 文件包含签名和年龄值。 .Exe 或.dll 文件相匹配的.pdb 文件中复制这些值。 在准备数据源之前, 此方法验证命名的.pdb 文件的签名和年龄匹配提供的值。  
  
 若要加载的.pdb 文件而不进行验证，请使用[idiadatasource:: Loaddatafrompdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)方法。  
  
 若要访问的数据加载过程 （通过一种回调机制），请使用[idiadatasource:: Loaddataforexe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)方法。  
  
 若要直接从内存加载的.pdb 文件，请使用[idiadatasource:: Loaddatafromistream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)方法。  
  
## <a name="example"></a>示例  
  
```cpp#  
IDiaDataSource* pSource;  // Previously created data source.  
DEFINE_GUID(expectedGUIDSignature,0x1234,0x5678,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08);  
DWORD expectedFileSignature = 0x12345678;  
DWORD expectedAge           = 128;  
  
HRESULT hr;  
hr = pSource->loadAndValidateDataFromPdb( L"yprog.pdb",  
                                          &expectedGUIDSignature,  
                                          expectedFileSignature,  
                                          expectedAge);  
if (FAILED(hr))  
{  
    // Report an error  
}  
  
```  
  
## <a name="see-also"></a>请参阅  
 [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)   
 [Idiadatasource:: Loaddataforexe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)   
 [Idiadatasource:: Loaddatafrompdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)   
 [IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)


