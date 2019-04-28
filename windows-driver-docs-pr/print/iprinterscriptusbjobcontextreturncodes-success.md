---
title: IPrinterScriptUsbJobContextReturnCodes Success 方法
description: 返回值为零 (0) 以通知 USBMon 函数调用已成功完成。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 783F9BCA-468E-4505-A6F3-9592D400E62C
keywords:
- Success 方法打印设备
- Success 方法打印设备，IPrinterScriptUsbJobContextReturnCodes 接口
- IPrinterScriptUsbJobContextReturnCodes 接口打印设备，Success 方法
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContextReturnCodes.Success
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abb415848c70a67db17c5c1163a9e3630839edf8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349224"
---
# <a name="iprinterscriptusbjobcontextreturncodessuccess-method"></a>IPrinterScriptUsbJobContextReturnCodes::Success 方法

返回值为零 (0) 以通知 USBMon 函数调用已成功完成。

<a name="syntax"></a>语法
------

```cpp
HRESULT Success(
  [out, retval] UINT32 *value
);
```

<a name="parameters"></a>Parameters
----------

*值* \[out，retval\]  
值，该值指示方法调用运行成功。

<a name="return-value"></a>返回值
------------

此方法返回**HRESULT**值。

<a name="remarks"></a>备注
-------

**成功**是只读的方法。

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

## <a name="see-also"></a>请参阅

[**IPrinterScriptUsbJobContextReturnCodes**](iprinterscriptusbjobcontextreturncodes.md)
