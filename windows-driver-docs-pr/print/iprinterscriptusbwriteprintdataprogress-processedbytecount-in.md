---
title: IPrinterScriptUsbWritePrintDataProgress ProcessedByteCount 方法
description: 设置 IHV JavaScript 函数在调用此方法时已处理的字节数。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 9E870B80-421B-496A-9510-D97D3A4D7892
keywords:
- ProcessedByteCount 方法打印设备
- ProcessedByteCount 方法打印设备，IPrinterScriptUsbWritePrintDataProgress 接口
- IPrinterScriptUsbWritePrintDataProgress 接口打印设备，ProcessedByteCount 方法
topic_type:
- apiref
api_name:
- IPrinterScriptUsbWritePrintDataProgress.ProcessedByteCount
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27d84b37a5863ca6acc3f9a080d94c78795d410f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547228"
---
# <a name="iprinterscriptusbwriteprintdataprogressprocessedbytecount-method"></a>IPrinterScriptUsbWritePrintDataProgress::ProcessedByteCount 方法

设置 IHV JavaScript 函数在调用此方法时已处理的字节数。

<a name="syntax"></a>语法
------

```cpp
HRESULT ProcessedByteCount(
  [in]  UINT32 value
);
```

<a name="parameters"></a>参数
----------

*value* \[in\]  
在调用此方法时处理的字节数。

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
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td><p>目标平台</p></td>
<td>桌面设备</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**IPrinterScriptUsbWritePrintDataProgress**](iprinterscriptusbwriteprintdataprogress.md)
