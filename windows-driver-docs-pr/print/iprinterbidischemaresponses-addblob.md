---
title: IPrinterBidiSchemaResponses AddBlob 方法
description: AddBlob 方法将添加新的响应的类型 BIDI\_到集合的 BLOB。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 9CB33F44-5DB8-4504-AD88-AEBE99C1E527
keywords:
- AddBlob 方法打印设备
- AddBlob 方法打印设备，IPrinterBidiSchemaResponses 接口
- IPrinterBidiSchemaResponses 接口打印设备，AddBlob 方法
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses.AddBlob
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5bf5d1d44db427dd71efd043be9ef97523b297c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567795"
---
# <a name="iprinterbidischemaresponsesaddblob-method"></a>IPrinterBidiSchemaResponses::AddBlob 方法

AddBlob 方法将添加新的响应的类型 BIDI\_到集合的 BLOB。

<a name="syntax"></a>语法
------

```cpp
HRESULT AddBlob(
  [in] BSTR      bstrSchema,
  [in] IDispatch *pArray
);
```

<a name="parameters"></a>Parameters
----------

*bstrSchema* \[in\]  
架构。

*pArray* \[in\]  
数组中。

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
<td><p>版本</p></td>
<td><p>Windows 8 及更高版本</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**IPrinterBidiSchemaResponses**](iprinterbidischemaresponses.md)
