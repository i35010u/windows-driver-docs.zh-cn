---
title: IPrinterScriptUsbJobContextReturnCodes AbortTheJob 方法
description: 返回的值为"4"，以通知 USBMon 必须中止该打印作业。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 6E56330E-BDD9-4EDC-A006-CA1D8A58DE32
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
ms.openlocfilehash: 873a13cc76aad4a0e4723eb47d5ab3d9e515bb32
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547055"
---
# <a name="iprinterscriptusbjobcontextreturncodesabortthejob-method"></a>IPrinterScriptUsbJobContextReturnCodes::AbortTheJob 方法

返回的值为"4"，以通知 USBMon 必须中止该打印作业。

<a name="syntax"></a>语法
------

```cpp
HRESULT AbortTheJob(
  [out, retval] UINT32 *value
);
```

<a name="parameters"></a>参数
----------

*值* \[out，retval\]  
值，该值指示打印作业必须被中止。

<a name="return-value"></a>返回值
------------

此方法返回**HRESULT**值。

<a name="remarks"></a>备注
-------

**AbortTheJob**是只读的方法。 从 IHV JavaScript 函数的此返回代码通知 USBMon 的设备无法继续处理该作业，或用户取消了该设备的前面板上的作业。 当 USBMon 收到的消息中止打印作业时，它将信息传递到打印后台处理程序中止作业，然后再返回。

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
