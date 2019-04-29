---
title: IPrinterBidiSchemaElement BidiType 方法
description: BidiType 方法返回 Bidi 架构元素类型。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 7E074633-E3AA-45F3-A0B6-621E97E983A8
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
ms.openlocfilehash: d7271f72d0ea0d010a4c8a15549f99dbdfd8f91e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371205"
---
# <a name="iprinterbidischemaelementbiditype-method"></a>IPrinterBidiSchemaElement::BidiType 方法

BidiType 方法返回 Bidi 架构元素类型。

<a name="syntax"></a>语法
------

```cpp
HRESULT BidiType(
  [out, retval] PrinterBidiSchemaElementType *pType
);
```

<a name="parameters"></a>Parameters
----------

*pType* \[out, retval\]  
返回的元素类型。

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

[**IPrinterBidiSchemaElement**](iprinterbidischemaelement-interface.md)

[**PrinterBidiSchemaElementType**](printerbidischemaelementtype.md)
