---
title: IPrinterBidiSchemaElement BidiType 方法
description: BidiType 方法返回双向架构元素类型。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- BidiType 方法打印设备
- BidiType 方法打印设备，IPrinterBidiSchemaElement 接口
- IPrinterBidiSchemaElement 接口打印设备，BidiType 方法
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaElement.BidiType
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: deae0a43be629aff0be3aa373e494af4b2b366e3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835601"
---
# <a name="iprinterbidischemaelementbiditype-method"></a>IPrinterBidiSchemaElement：： BidiType 方法

BidiType 方法返回双向架构元素类型。

<a name="syntax"></a>语法
------

```cpp
HRESULT BidiType(
  [out, retval] PrinterBidiSchemaElementType *pType
);
```

<a name="parameters"></a>参数
----------

*pType* \[out，retval\]  
返回的元素类型。

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

[**IPrinterBidiSchemaElement**](iprinterbidischemaelement-interface.md)

[**PrinterBidiSchemaElementType**](printerbidischemaelementtype.md)
