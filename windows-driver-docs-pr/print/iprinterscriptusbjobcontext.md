---
title: IPrinterScriptUsbJobContext 接口
description: IPrinterScriptUsbJobContext 接口作为参数传递给 startPrintJob JavaScript 函数。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 236F6B00-39D8-4084-BAE0-C349AD550040
keywords:
- IPrinterScriptUsbJobContext 接口打印设备
- IPrinterScriptUsbJobContext 接口打印设备，描述
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContext
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10b521ad8d1b50b75b9480cac14b6f920e2e12e8
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802757"
---
# <a name="iprinterscriptusbjobcontext-interface"></a>IPrinterScriptUsbJobContext 接口

IPrinterScriptUsbJobContext 接口作为参数传递给 **startPrintJob** JavaScript 函数。

<a name="members"></a>成员
-------

**IPrinterScriptUsbJobContext**接口继承自[**IUnknown**](https://docs.microsoft.com/windows/win32/api/unknwn/nn-unknwn-iunknown)接口。 **IPrinterScriptUsbJobContext** 还具有下列类型的成员：

-   [方法](#methods)

### <a name="methods"></a>方法

**IPrinterScriptUsbJobContext**接口具有这些方法。

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
<td><a href="iprinterscriptusbjobcontext-jobpropertybag.md" data-raw-source="[&lt;strong&gt;JobPropertyBag&lt;/strong&gt;](iprinterscriptusbjobcontext-jobpropertybag.md)"><strong>JobPropertyBag</strong></a></td>
<td><p>返回与当前打印作业关联的属性包。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterscriptusbjobcontext-printedpagecount.md" data-raw-source="[&lt;strong&gt;PrintedPageCount&lt;/strong&gt;](iprinterscriptusbjobcontext-printedpagecount.md)"><strong>PrintedPageCount</strong></a></td>
<td><p>返回当前作业中打印设备打印的页数。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterscriptusbjobcontext-printedpagecount-in.md" data-raw-source="[&lt;strong&gt;PrintedPageCount&lt;/strong&gt;](iprinterscriptusbjobcontext-printedpagecount-in.md)"><strong>PrintedPageCount</strong></a></td>
<td><p>设置在当前作业中打印设备打印的页数。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterscriptusbjobcontext-returncodes.md" data-raw-source="[&lt;strong&gt;ReturnCodes&lt;/strong&gt;](iprinterscriptusbjobcontext-returncodes.md)"><strong>ReturnCodes</strong></a></td>
<td><p>返回一个对象，该对象可提供 IHV 为其 JavaScript 函数定义的返回代码值。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterscriptusbjobcontext-temporarystreams.md" data-raw-source="[&lt;strong&gt;TemporaryStreams&lt;/strong&gt;](iprinterscriptusbjobcontext-temporarystreams.md)"><strong>TemporaryStreams</strong></a></td>
<td><p>返回可由 IHV JavaScript 函数为当前作业使用的永久性数据流的 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream" data-raw-source="[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream)">IPrinterScriptableSequentialStream</a> 接口的数组。</p></td>
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
