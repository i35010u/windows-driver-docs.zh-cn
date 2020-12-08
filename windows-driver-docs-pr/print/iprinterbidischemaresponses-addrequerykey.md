---
title: IPrinterBidiSchemaResponses AddRequeryKey 方法
description: AddRequeryKey 方法添加新的查询密钥，以在从 getSchemas 调用返回时重新查询。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- AddRequeryKey 方法打印设备
- AddRequeryKey 方法打印设备，IPrinterBidiSchemaResponses 接口
- IPrinterBidiSchemaResponses 接口打印设备，AddRequeryKey 方法
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses.AddRequeryKey
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9eee89b72ffa11d129979806bf1fd0c1a4037b92
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835569"
---
# <a name="iprinterbidischemaresponsesaddrequerykey-method"></a>IPrinterBidiSchemaResponses：： AddRequeryKey 方法

AddRequeryKey 方法添加新的查询密钥，以在从 getSchemas 调用返回时重新查询。

<a name="syntax"></a>语法
------

```cpp
HRESULT AddRequeryKey(
  [in] BSTR   bstrQueryKey
);
```

<a name="parameters"></a>参数
----------

 *bstrQueryKey* \[中\]  
新查询密钥。

<a name="return-value"></a>返回值
------------

此方法返回 **HRESULT** 值。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>目标平台</p></td>
<td>台式机</td>
</tr>
<tr class="even">
<td><p>版本</p></td>
<td><p>Windows 8 及更高版本</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**IPrinterBidiSchemaResponses**](iprinterbidischemaresponses.md)
