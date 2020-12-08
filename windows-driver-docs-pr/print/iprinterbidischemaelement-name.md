---
title: IPrinterBidiSchemaElement Name 方法
description: Name 方法返回双向架构元素名称。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- 命名方法打印设备
- 命名方法打印设备，IPrinterBidiSchemaElement 接口
- IPrinterBidiSchemaElement 接口打印设备，Name 方法
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaElement.Name
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3e167fa754f6d0d835cec0c0caaf4ce1b9c87f7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835593"
---
# <a name="iprinterbidischemaelementname-method"></a>IPrinterBidiSchemaElement：： Name 方法

Name 方法返回双向架构元素名称。

<a name="syntax"></a>语法
------

```cpp
HRESULT Name(
  [out, retval] BSTR *pbstrSchema
);
```

<a name="parameters"></a>参数
----------

*pbstrSchema* \[out，retval\]  
返回的元素名称。

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
