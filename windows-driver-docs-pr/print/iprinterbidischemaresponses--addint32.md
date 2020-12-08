---
title: IPrinterBidiSchemaResponses AddInt32 方法
description: AddInt32 方法将一个双向 INT 类型的新响应添加 \_ 到集合中。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- AddInt32 方法打印设备
- AddInt32 方法打印设备，IPrinterBidiSchemaResponses 接口
- IPrinterBidiSchemaResponses 接口打印设备，AddInt32 方法
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses.AddInt32
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1c37a0be56c38ba771de980894c1595a3ade540
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796625"
---
# <a name="iprinterbidischemaresponsesaddint32-method"></a>IPrinterBidiSchemaResponses：： AddInt32 方法

AddInt32 方法将一个双向 INT 类型的新响应添加 \_ 到集合中。

<a name="syntax"></a>语法
------

```cpp
HRESULT  AddInt32(
  [in] BSTR bstrSchema,
  [in] LONG lValue
);
```

<a name="parameters"></a>参数
----------

*bstrSchema* \[中\]  
架构。

*lValue* \[中\]  
新值。

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
