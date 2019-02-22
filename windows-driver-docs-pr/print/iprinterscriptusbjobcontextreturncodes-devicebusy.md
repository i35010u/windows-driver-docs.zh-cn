---
title: IPrinterScriptUsbJobContextReturnCodes DeviceBusy 方法
description: 返回一个值"3"，以通知 USBMon 设备通信通道这次不接受数据。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: D1205445-2587-4C9D-B383-587F06A3E899
keywords:
- DeviceBusy 方法打印设备
- DeviceBusy 方法打印设备，IPrinterScriptUsbJobContextReturnCodes 接口
- IPrinterScriptUsbJobContextReturnCodes 接口打印设备，DeviceBusy 方法
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContextReturnCodes.DeviceBusy
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 437e48ed6f6a274b92751d32f40d2cb58580835c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524867"
---
# <a name="iprinterscriptusbjobcontextreturncodesdevicebusy-method"></a>IPrinterScriptUsbJobContextReturnCodes::DeviceBusy 方法

返回一个值"3"，以通知 USBMon 设备通信通道这次不接受数据。

<a name="syntax"></a>语法
------

```cpp
HRESULT DeviceBusy(
  [out, retval] UINT32 *value
);
```

<a name="parameters"></a>参数
----------

*值* \[out，retval\]  
值，该值指示信道这次不接受数据。

<a name="return-value"></a>返回值
------------

此方法返回**HRESULT**值。

<a name="remarks"></a>备注
-------

**DeviceBusy**是只读的方法。 返回的值为"3"并不表示失败，并 USBMon 应通知打印后台处理程序设备正忙。 USBMon 然后可以在更高版本时再次调用函数。 从打印数据流 (printData) 处理的字节数是 writePrintDataProgress 对象中返回。

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

[**IPrinterScriptUsbJobContextReturnCodes**](iprinterscriptusbjobcontextreturncodes.md)
