---
title: IPrinterScriptUsbJobContextReturnCodes 接口
description: IPrinterScriptUsbJobContextReturnCodes 接口表示 IHV 为其 JavaScript 函数定义的一系列返回代码。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 8E34748E-B9F9-4404-9B40-04EA72EEA322
keywords:
- IPrinterScriptUsbJobContextReturnCodes 接口打印设备
- IPrinterScriptUsbJobContextReturnCodes 接口打印设备，描述
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContextReturnCodes
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bf16113db3441f950e805b3a39d927d64c2f909
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217151"
---
# <a name="iprinterscriptusbjobcontextreturncodes-interface"></a>IPrinterScriptUsbJobContextReturnCodes 接口

IPrinterScriptUsbJobContextReturnCodes 接口表示 IHV 为其 JavaScript 函数定义的一系列返回代码。

此接口由 [**IPrinterScriptUsbJobContext：： ReturnCodes**](iprinterscriptusbjobcontext-returncodes.md) 方法返回。

<a name="members"></a>成员
-------

**IPrinterScriptUsbJobContextReturnCodes**接口继承自[**IUnknown**](/windows/win32/api/unknwn/nn-unknwn-iunknown)接口。 **IPrinterScriptUsbJobContextReturnCodes** 还具有下列类型的成员：

-   [方法](#methods)

### <a name="methods"></a>方法

**IPrinterScriptUsbJobContextReturnCodes**接口具有这些方法。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="iprinterscriptusbjobcontextreturncodes-abortthejob.md" data-raw-source="[&lt;strong&gt;AbortTheJob&lt;/strong&gt;](iprinterscriptusbjobcontextreturncodes-abortthejob.md)"><strong>AbortTheJob</strong></a></td>
<td><p>返回值 "4"，通知 USBMon 必须中止打印作业。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterscriptusbjobcontextreturncodes-devicebusy.md" data-raw-source="[&lt;strong&gt;DeviceBusy&lt;/strong&gt;](iprinterscriptusbjobcontextreturncodes-devicebusy.md)"><strong>DeviceBusy</strong></a></td>
<td><p>返回值 "3"，通知 USBMon 设备通信通道目前不接受数据。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterscriptusbjobcontextreturncodes-failure.md" data-raw-source="[&lt;strong&gt;Failure&lt;/strong&gt;](iprinterscriptusbjobcontextreturncodes-failure.md)"><strong>失败</strong></a></td>
<td><p>返回值 "1"，通知 USBMon 方法调用失败。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterscriptusbjobcontextreturncodes-retry.md" data-raw-source="[&lt;strong&gt;Retry&lt;/strong&gt;](iprinterscriptusbjobcontextreturncodes-retry.md)"><strong>重试</strong></a></td>
<td><p>返回值 "2"，通知 USBMon 方法调用成功，同时完成更多的工作。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterscriptusbjobcontextreturncodes-success.md" data-raw-source="[&lt;strong&gt;Success&lt;/strong&gt;](iprinterscriptusbjobcontextreturncodes-success.md)"><strong>成功</strong></a></td>
<td><p>返回值为零 (0) 通知 USBMon 函数调用已成功完成。</p></td>
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
<td><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2012 R2</p></td>
</tr>
</tbody>
</table>