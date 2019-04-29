---
title: IPrinterScriptUsbJobContextReturnCodes 重试方法
description: 返回"2"，以通知 USBMon 方法调用已成功，与更多工作要完成的值。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 1EDF5EFA-1158-4BC7-99AB-3811E4443E62
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
ms.openlocfilehash: 436e2b14d2e82fb2208e9dd6bbe81344b61535f4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349215"
---
# <a name="iprinterscriptusbjobcontextreturncodesretry-method"></a>IPrinterScriptUsbJobContextReturnCodes::Retry 方法

返回"2"，以通知 USBMon 方法调用已成功，与更多工作要完成的值。

<a name="syntax"></a>语法
------

```cpp
HRESULT Retry(
  [out, retval] UINT32 *value
);
```

<a name="parameters"></a>Parameters
----------

*值* \[out，retval\]  
值，该值指示方法调用运行成功，与更多的工作来完成。

<a name="return-value"></a>返回值
------------

此方法返回**HRESULT**值。

<a name="remarks"></a>备注
-------

**重试**是只读的方法。 应在 printerBidiSchemaResponses 对象中，处理任何 Bidi 架构更新 （包括 Bidi 事件），然后调用 USBMon**重试**方法再次以允许 IHV 代码以继续处理数据。 从打印数据流 (printData) 处理的字节数与打印作业相关联的 writePrintDataProgress 对象中返回。

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
