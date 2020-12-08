---
title: IPrinterScriptUsbJobContextReturnCodes 重试方法
description: 返回值 "2"，通知 USBMon 方法调用成功，同时完成更多的工作。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- 重试方法打印设备
- 重试方法打印设备，IPrinterScriptUsbJobContextReturnCodes 接口
- IPrinterScriptUsbJobContextReturnCodes 接口打印设备，重试方法
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContextReturnCodes.Retry
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60749b6c92d2d18e4b4696ef29b57915a1d91786
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835543"
---
# <a name="iprinterscriptusbjobcontextreturncodesretry-method"></a>IPrinterScriptUsbJobContextReturnCodes：： Retry 方法

返回值 "2"，通知 USBMon 方法调用成功，同时完成更多的工作。

<a name="syntax"></a>语法
------

```cpp
HRESULT Retry(
  [out, retval] UINT32 *value
);
```

<a name="parameters"></a>参数
----------

*值* \[out，retval\]  
指示成功方法调用的值，以及要完成的工作。

<a name="return-value"></a>返回值
------------

此方法返回 **HRESULT** 值。

<a name="remarks"></a>备注
-------

**Retry** 为只读方法。 USBMon 应) 在 printerBidiSchemaResponses 对象中处理 (包括双向事件，并再次调用 **Retry** 方法，以允许 IHV 代码继续处理数据。 在与打印作业关联的 writePrintDataProgress 对象中返回从打印数据流)  (的字节数。

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
