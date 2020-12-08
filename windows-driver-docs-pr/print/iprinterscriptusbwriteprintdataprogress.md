---
title: IPrinterScriptUsbWritePrintDataProgress 接口
description: IPrinterScriptUsbWritePrintDataProgress 接口作为参数传递到 writePrintData JavaScript 函数调用中。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
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
ms.openlocfilehash: 48d16e68ad5e55ad39daa5b04811500a086b9edf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796569"
---
# <a name="iprinterscriptusbwriteprintdataprogress-interface"></a>IPrinterScriptUsbWritePrintDataProgress 接口

IPrinterScriptUsbWritePrintDataProgress 接口作为参数传递到 **writePrintData** JavaScript 函数调用中。

<a name="members"></a>成员
-------

**IPrinterScriptUsbWritePrintDataProgress** 接口继承自 [**IUnknown**](/windows/win32/api/unknwn/nn-unknwn-iunknown)接口。 **IPrinterScriptUsbWritePrintDataProgress** 还具有下列类型的成员：

-   [方法](#methods)

### <a name="methods"></a>方法

**IPrinterScriptUsbWritePrintDataProgress** 接口具有这些方法。

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
<td><a href="iprinterscriptusbwriteprintdataprogress-processedbytecount.md" data-raw-source="[&lt;strong&gt;ProcessedByteCount&lt;/strong&gt;](iprinterscriptusbwriteprintdataprogress-processedbytecount.md)"><strong>ProcessedByteCount</strong></a></td>
<td><p>返回在调用此方法时由 IHV JavaScript 函数处理的字节数。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterscriptusbwriteprintdataprogress-processedbytecount-in.md" data-raw-source="[&lt;strong&gt;ProcessedByteCount&lt;/strong&gt;](iprinterscriptusbwriteprintdataprogress-processedbytecount-in.md)"><strong>ProcessedByteCount</strong></a></td>
<td><p>设置在调用此方法时 IHV JavaScript 函数已处理的字节数。</p></td>
</tr>
</tbody>
</table>
