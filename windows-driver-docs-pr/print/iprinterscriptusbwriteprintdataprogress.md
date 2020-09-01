---
title: IPrinterScriptUsbWritePrintDataProgress 接口
description: IPrinterScriptUsbWritePrintDataProgress 接口作为参数传递到 writePrintData JavaScript 函数调用中。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: E22725DA-2BD5-4FBC-A3E4-A3C5678A9E57
keywords:
- IPrinterScriptUsbWritePrintDataProgress 接口打印设备
- IPrinterScriptUsbWritePrintDataProgress 接口打印设备，描述
topic_type:
- apiref
api_name:
- IPrinterScriptUsbWritePrintDataProgress
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea97f08ef37fec791cb8056d51cab5407adda024
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217122"
---
# <a name="iprinterscriptusbwriteprintdataprogress-interface"></a>IPrinterScriptUsbWritePrintDataProgress 接口

IPrinterScriptUsbWritePrintDataProgress 接口作为参数传递到 **writePrintData** JavaScript 函数调用中。

<a name="members"></a>成员
-------

**IPrinterScriptUsbWritePrintDataProgress**接口继承自[**IUnknown**](/windows/win32/api/unknwn/nn-unknwn-iunknown)接口。 **IPrinterScriptUsbWritePrintDataProgress** 还具有下列类型的成员：

-   [方法](#methods)

### <a name="methods"></a>方法

**IPrinterScriptUsbWritePrintDataProgress**接口具有这些方法。

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
<td><a href="iprinterscriptusbwriteprintdataprogress-processedbytecount.md" data-raw-source="[&lt;strong&gt;ProcessedByteCount&lt;/strong&gt;](iprinterscriptusbwriteprintdataprogress-processedbytecount.md)"><strong>ProcessedByteCount</strong></a></td>
<td><p>返回在调用此方法时由 IHV JavaScript 函数处理的字节数。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterscriptusbwriteprintdataprogress-processedbytecount-in.md" data-raw-source="[&lt;strong&gt;ProcessedByteCount&lt;/strong&gt;](iprinterscriptusbwriteprintdataprogress-processedbytecount-in.md)"><strong>ProcessedByteCount</strong></a></td>
<td><p>设置在调用此方法时 IHV JavaScript 函数已处理的字节数。</p></td>
</tr>
</tbody>
</table>