---
title: IPrinterScriptUsbJobContextReturnCodes 失败方法
description: 返回值 "1"，通知 USBMon 方法调用失败。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- 故障方法打印设备
- 故障方法打印设备，IPrinterScriptUsbJobContextReturnCodes 接口
- IPrinterScriptUsbJobContextReturnCodes 接口打印设备，失败方法
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContextReturnCodes.Failure
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 955192d8c906e56946b281a9a14556e6441ac147
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796583"
---
# <a name="iprinterscriptusbjobcontextreturncodesfailure-method"></a>IPrinterScriptUsbJobContextReturnCodes：：失败方法

返回值 "1"，通知 USBMon 方法调用失败。

<a name="syntax"></a>语法
------

```cpp
HRESULT Failure(
  [out, retval] UINT32 *value
);
```

<a name="parameters"></a>参数
----------

*值* \[out，retval\]  
值，指示方法调用失败。

<a name="return-value"></a>返回值
------------

此方法返回 **HRESULT** 值。

<a name="remarks"></a>备注
-------

**故障** 为只读方法。 当 USBMon 收到此失败值时，它会清理作业上下文对象并将错误代码返回到打印后台处理程序。

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
