---
title: IPrinterBidiSchemaResponses AddRequeryKey 方法
description: AddRequeryKey 方法将添加新的查询密钥，以重新查询从 getSchemas 调用返回时。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: D2C418C4-3C1B-4CEA-9F39-036C4DB2A483
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
ms.openlocfilehash: 335f75d02acd7c6661a013aec81c2e4beb1898b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351655"
---
# <a name="iprinterbidischemaresponsesaddrequerykey-method"></a>IPrinterBidiSchemaResponses::AddRequeryKey 方法

AddRequeryKey 方法将添加新的查询密钥，以重新查询从 getSchemas 调用返回时。

<a name="syntax"></a>语法
------

```cpp
HRESULT AddRequeryKey(
  [in] BSTR   bstrQueryKey
);
```

<a name="parameters"></a>Parameters
----------

 *bstrQueryKey* \[in\]  
新的查询密钥。

<a name="return-value"></a>返回值
------------

此方法返回**HRESULT**值。

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
<td>桌面设备</td>
</tr>
<tr class="even">
<td><p>Version</p></td>
<td><p>Windows 8 及更高版本</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**IPrinterBidiSchemaResponses**](iprinterbidischemaresponses.md)
