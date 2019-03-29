---
title: IPrinterScriptUsbJobContextReturnCodes 接口
description: IPrinterScriptUsbJobContextReturnCodes 接口表示 IHV 已定义的 JavaScript 函数的返回代码的数组。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 8E34748E-B9F9-4404-9B40-04EA72EEA322
keywords:
- IPrinterScriptUsbJobContextReturnCodes 接口打印设备
- IPrinterScriptUsbJobContextReturnCodes 接口所述的打印设备
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContextReturnCodes
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09802d98945e348e23c02d4377f4b09b607c5a59
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350092"
---
# <a name="iprinterscriptusbjobcontextreturncodes-interface"></a>IPrinterScriptUsbJobContextReturnCodes 接口

IPrinterScriptUsbJobContextReturnCodes 接口表示 IHV 已定义的 JavaScript 函数的返回代码的数组。

此接口将返回由[ **IPrinterScriptUsbJobContext::ReturnCodes** ](iprinterscriptusbjobcontext-returncodes.md)方法。

<a name="members"></a>成员
-------

**IPrinterScriptUsbJobContextReturnCodes**接口继承自[ **IUnknown** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)接口。 **IPrinterScriptUsbJobContextReturnCodes**还具有这些类型的成员：

-   [方法](#methods)

### <a name="methods"></a>方法

**IPrinterScriptUsbJobContextReturnCodes**接口提供以下方法。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="iprinterscriptusbjobcontextreturncodes-abortthejob.md" data-raw-source="[&lt;strong&gt;AbortTheJob&lt;/strong&gt;](iprinterscriptusbjobcontextreturncodes-abortthejob.md)"><strong>AbortTheJob</strong></a></td>
<td><p>返回的值为"4"，以通知 USBMon 必须中止该打印作业。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterscriptusbjobcontextreturncodes-devicebusy.md" data-raw-source="[&lt;strong&gt;DeviceBusy&lt;/strong&gt;](iprinterscriptusbjobcontextreturncodes-devicebusy.md)"><strong>DeviceBusy</strong></a></td>
<td><p>返回一个值"3"，以通知 USBMon 设备通信通道这次不接受数据。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterscriptusbjobcontextreturncodes-failure.md" data-raw-source="[&lt;strong&gt;Failure&lt;/strong&gt;](iprinterscriptusbjobcontextreturncodes-failure.md)"><strong>失败</strong></a></td>
<td><p>返回一个值"1"，以通知 USBMon 方法调用失败。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterscriptusbjobcontextreturncodes-retry.md" data-raw-source="[&lt;strong&gt;Retry&lt;/strong&gt;](iprinterscriptusbjobcontextreturncodes-retry.md)"><strong>Retry</strong></a></td>
<td><p>返回"2"，以通知 USBMon 方法调用已成功，与更多工作要完成的值。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterscriptusbjobcontextreturncodes-success.md" data-raw-source="[&lt;strong&gt;Success&lt;/strong&gt;](iprinterscriptusbjobcontextreturncodes-success.md)"><strong>Success</strong></a></td>
<td><p>返回值为零 (0) 以通知 USBMon 函数调用已成功完成。</p></td>
</tr>
</tbody>
</table>

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
</tbody>
</table>
