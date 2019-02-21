---
title: IPrinterScriptUsbJobContext 接口
description: IPrinterScriptUsbJobContext 接口作为参数传递给 startPrintJob JavaScript 函数。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 236F6B00-39D8-4084-BAE0-C349AD550040
keywords:
- IPrinterScriptUsbJobContext 接口打印设备
- 描述 IPrinterScriptUsbJobContext 接口打印设备
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContext
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f662d41a3ccfad4852054ec9b36d28fae2aed89b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521221"
---
# <a name="iprinterscriptusbjobcontext-interface"></a>IPrinterScriptUsbJobContext 接口

IPrinterScriptUsbJobContext 接口作为参数传递给**startPrintJob** JavaScript 函数。

<a name="members"></a>成员
-------

**IPrinterScriptUsbJobContext**接口继承自[ **IUnknown** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)接口。 **IPrinterScriptUsbJobContext**还具有这些类型的成员：

-   [方法](#methods)

### <a name="methods"></a>方法

**IPrinterScriptUsbJobContext**接口提供以下方法。

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
<td><a href="iprinterscriptusbjobcontext-jobpropertybag.md" data-raw-source="[&lt;strong&gt;JobPropertyBag&lt;/strong&gt;](iprinterscriptusbjobcontext-jobpropertybag.md)"><strong>JobPropertyBag</strong></a></td>
<td><p>返回与当前打印作业相关联的属性包。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterscriptusbjobcontext-printedpagecount.md" data-raw-source="[&lt;strong&gt;PrintedPageCount&lt;/strong&gt;](iprinterscriptusbjobcontext-printedpagecount.md)"><strong>PrintedPageCount</strong></a></td>
<td><p>返回由当前的作业中的打印设备打印的页数。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterscriptusbjobcontext-printedpagecount-in.md" data-raw-source="[&lt;strong&gt;PrintedPageCount&lt;/strong&gt;](iprinterscriptusbjobcontext-printedpagecount-in.md)"><strong>PrintedPageCount</strong></a></td>
<td><p>设置由当前的作业中的打印设备打印的页数。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterscriptusbjobcontext-returncodes.md" data-raw-source="[&lt;strong&gt;ReturnCodes&lt;/strong&gt;](iprinterscriptusbjobcontext-returncodes.md)"><strong>ReturnCodes</strong></a></td>
<td><p>返回一个对象，可以提供 IHV 已定义的 JavaScript 函数的返回代码值。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterscriptusbjobcontext-temporarystreams.md" data-raw-source="[&lt;strong&gt;TemporaryStreams&lt;/strong&gt;](iprinterscriptusbjobcontext-temporarystreams.md)"><strong>TemporaryStreams</strong></a></td>
<td><p>返回的数组<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptablesequentialstream" data-raw-source="[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptablesequentialstream)">IPrinterScriptableSequentialStream</a>持久性数据流可用于当前作业由 IHV JavaScript 函数的接口。</p></td>
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
