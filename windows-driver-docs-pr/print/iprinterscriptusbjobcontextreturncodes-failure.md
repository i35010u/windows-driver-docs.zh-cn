---
title: IPrinterScriptUsbJobContextReturnCodes Failure 方法
description: 返回一个值"1"，以通知 USBMon 方法调用失败。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: EEFDB8CA-5B6F-46E5-B181-074354E8B0EE
keywords:
- Failure 方法打印设备
- Failure 方法打印设备，IPrinterScriptUsbJobContextReturnCodes 接口
- IPrinterScriptUsbJobContextReturnCodes 接口打印设备，失败方法
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContextReturnCodes.Failure
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d5eeb76d2e3152c564f23eeec6a370c244d5f00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562326"
---
# <a name="iprinterscriptusbjobcontextreturncodesfailure-method"></a>IPrinterScriptUsbJobContextReturnCodes::Failure 方法

返回一个值"1"，以通知 USBMon 方法调用失败。

<a name="syntax"></a>语法
------

```cpp
HRESULT Failure(
  [out, retval] UINT32 *value
);
```

<a name="parameters"></a>Parameters
----------

*值* \[out，retval\]  
值，该值指示失败的方法调用。

<a name="return-value"></a>返回值
------------

此方法返回**HRESULT**值。

<a name="remarks"></a>备注
-------

**失败**是只读的方法。 当 USBMon 收到此失败值时，它会清除作业上下文对象并将错误代码返回到打印后台处理程序。

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
