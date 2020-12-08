---
title: IPrinterScriptUsbJobContextReturnCodes AbortTheJob 方法
description: 返回值 "4"，通知 USBMon 必须中止打印作业。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- AbortTheJob 方法打印设备
- AbortTheJob 方法打印设备，IPrinterScriptUsbJobContextReturnCodes 接口
- IPrinterScriptUsbJobContextReturnCodes 接口打印设备，AbortTheJob 方法
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContextReturnCodes.AbortTheJob
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11fbbd1d4063aed11a6d4e82388ff0ebc467a91b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796587"
---
# <a name="iprinterscriptusbjobcontextreturncodesabortthejob-method"></a>IPrinterScriptUsbJobContextReturnCodes：： AbortTheJob 方法

返回值 "4"，通知 USBMon 必须中止打印作业。

<a name="syntax"></a>语法
------

```cpp
HRESULT AbortTheJob(
  [out, retval] UINT32 *value
);
```

<a name="parameters"></a>参数
----------

*值* \[out，retval\]  
指示打印作业必须中止的值。

<a name="return-value"></a>返回值
------------

此方法返回 **HRESULT** 值。

<a name="remarks"></a>备注
-------

**AbortTheJob** 为只读方法。 以下来自 IHV JavaScript 函数的返回代码通知 USBMon：设备无法继续处理作业，或者用户已取消设备的前面板上的作业。 当 USBMon 收到用于中止打印作业的消息时，它会将信息传递给打印后台处理程序，以在返回前中止作业。

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
