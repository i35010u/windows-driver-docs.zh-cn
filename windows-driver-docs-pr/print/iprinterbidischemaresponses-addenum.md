---
title: IPrinterBidiSchemaResponses AddEnum 方法
description: AddEnum 方法将一个双向枚举类型的新响应添加 \_ 到集合中。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- AddEnum 方法打印设备
- AddEnum 方法打印设备，IPrinterBidiSchemaResponses 接口
- IPrinterBidiSchemaResponses 接口打印设备，AddEnum 方法
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses.AddEnum
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83863310eeee41d76c71c3be6179e88a5a8c74b4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796623"
---
# <a name="iprinterbidischemaresponsesaddenum-method"></a>IPrinterBidiSchemaResponses：： AddEnum 方法

AddEnum 方法将一个双向枚举类型的新响应添加 \_ 到集合中。

<a name="syntax"></a>语法
------

```cpp
HRESULT AddEnum(
  [in] BSTR bstrSchema,
  [in] BSTR bstrValue
);
```

<a name="parameters"></a>参数
----------

*bstrSchema* \[中\]  
架构。

*bstrValue* \[中\]  
枚举值。

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
