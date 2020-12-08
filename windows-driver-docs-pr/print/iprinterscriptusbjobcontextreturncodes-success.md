---
title: IPrinterScriptUsbJobContextReturnCodes Success 方法
description: 返回值为零 (0) 通知 USBMon 函数调用已成功完成。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- 成功方法打印设备
- 成功方法打印设备，IPrinterScriptUsbJobContextReturnCodes 接口
- IPrinterScriptUsbJobContextReturnCodes 接口打印设备，Success 方法
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContextReturnCodes.Success
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b25176ba5ef0ad11af5be7f27cafa6c905081e39
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796585"
---
# <a name="iprinterscriptusbjobcontextreturncodessuccess-method"></a>IPrinterScriptUsbJobContextReturnCodes：： Success 方法

返回值为零 (0) 通知 USBMon 函数调用已成功完成。

<a name="syntax"></a>语法
------

```cpp
HRESULT Success(
  [out, retval] UINT32 *value
);
```

<a name="parameters"></a>参数
----------

*值* \[out，retval\]  
指示成功调用方法的值。

<a name="return-value"></a>返回值
------------

此方法返回 **HRESULT** 值。

<a name="remarks"></a>备注
-------

**Success** 为只读方法。

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
