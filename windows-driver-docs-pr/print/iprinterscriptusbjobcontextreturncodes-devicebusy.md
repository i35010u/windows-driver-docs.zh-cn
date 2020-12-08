---
title: IPrinterScriptUsbJobContextReturnCodes DeviceBusy 方法
description: 返回值 "3"，通知 USBMon 设备通信通道目前不接受数据。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
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
ms.openlocfilehash: e7a5b4c4809e9d6cf5d6c417336d7881561ed082
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835551"
---
# <a name="iprinterscriptusbjobcontextreturncodesdevicebusy-method"></a>IPrinterScriptUsbJobContextReturnCodes：:D eviceBusy 方法

返回值 "3"，通知 USBMon 设备通信通道目前不接受数据。

<a name="syntax"></a>语法
------

```cpp
HRESULT DeviceBusy(
  [out, retval] UINT32 *value
);
```

<a name="parameters"></a>参数
----------

*值* \[out，retval\]  
一个值，该值指示通信通道目前不接受数据。

<a name="return-value"></a>返回值
------------

此方法返回 **HRESULT** 值。

<a name="remarks"></a>备注
-------

**DeviceBusy** 为只读方法。 返回值 "3" 不表示失败，USBMon 应通知打印后台处理程序设备处于繁忙状态。 然后，USBMon 可以稍后再次调用该函数。 在 writePrintDataProgress 对象中返回 (printData) 从打印数据流处理的字节数。

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
<td>台式机</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**IPrinterScriptUsbJobContextReturnCodes**](iprinterscriptusbjobcontextreturncodes.md)
