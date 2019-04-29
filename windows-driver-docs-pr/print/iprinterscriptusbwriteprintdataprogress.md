---
title: IPrinterScriptUsbWritePrintDataProgress 接口
description: IPrinterScriptUsbWritePrintDataProgress 接口作为 writePrintData JavaScript 函数调用中的参数传递。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: E22725DA-2BD5-4FBC-A3E4-A3C5678A9E57
keywords:
- IPrinterScriptUsbWritePrintDataProgress 接口打印设备
- IPrinterScriptUsbWritePrintDataProgress 接口所述的打印设备
topic_type:
- apiref
api_name:
- IPrinterScriptUsbWritePrintDataProgress
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8330eb195ea94869a387d8939ba7c63fc9fdaa1f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349207"
---
# <a name="iprinterscriptusbwriteprintdataprogress-interface"></a>IPrinterScriptUsbWritePrintDataProgress 接口

作为中的参数传递 IPrinterScriptUsbWritePrintDataProgress 接口**writePrintData** JavaScript 函数调用。

<a name="members"></a>成员
-------

**IPrinterScriptUsbWritePrintDataProgress**接口继承自[ **IUnknown** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)接口。 **IPrinterScriptUsbWritePrintDataProgress**还具有这些类型的成员：

-   [方法](#methods)

### <a name="methods"></a>方法

**IPrinterScriptUsbWritePrintDataProgress**接口提供以下方法。

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
<td><p>返回 IHV JavaScript 函数调用此方法时已处理的字节的数。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterscriptusbwriteprintdataprogress-processedbytecount-in.md" data-raw-source="[&lt;strong&gt;ProcessedByteCount&lt;/strong&gt;](iprinterscriptusbwriteprintdataprogress-processedbytecount-in.md)"><strong>ProcessedByteCount</strong></a></td>
<td><p>设置 IHV JavaScript 函数在调用此方法时已处理的字节数。</p></td>
</tr>
</tbody>
</table>
