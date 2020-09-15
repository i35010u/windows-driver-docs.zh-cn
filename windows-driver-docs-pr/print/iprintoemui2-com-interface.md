---
title: IPrintOemUI2 COM 接口
description: IPrintOemUI2 COM 接口
ms.assetid: 9aee61af-e8e2-4bc4-a17b-783242d1ac1f
keywords:
- IPrintOemUI2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9b98c89df1fba6e0de859c841561de7c341872f
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105850"
---
# <a name="iprintoemui2-com-interface"></a>IPrintOemUI2 COM 接口





`IPrintOemUI2`Com 接口扩展了[IPrintOemUI com 接口](iprintoemui-com-interface.md)。 除了 **IPrintOemUI** 接口中的所有方法， `IPrintOemUI2` 接口还提供以下方法。

**注意**   如果使用的是 Windows Vista 版本的 Unidrv 和 Pscript Dll，则可以在 Windows XP 和更高版本的 Windows 操作系统上运行的 Unidrv 或 Pscript5 插件中实现以下方法。 以前版本的 Dll 仅支持 Pscript5 插件中的 **IPrintOEM2：： HideStandardUI** 方法。

 

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
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui2-documentevent" data-raw-source="[&lt;strong&gt;IPrintOemUI2::DocumentEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui2-documentevent)"><strong>IPrintOemUI2：:D ocumentEvent</strong></a></p></td>
<td><p>启用 UI 插件来替换核心驱动程序 UI 模块的 <a href="/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentevent" data-raw-source="[&lt;strong&gt;DrvDocumentEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentevent)"><strong>DrvDocumentEvent</strong></a> DDI 的默认实现。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui2-hidestandardui" data-raw-source="[&lt;strong&gt;IPrintOemUI2::HideStandardUI&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui2-hidestandardui)"><strong>IPrintOemUI2::HideStandardUI</strong></a></p></td>
<td><p>允许 UI 插件指定是应显示还是隐藏标准属性表。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui2-queryjobattributes" data-raw-source="[&lt;strong&gt;IPrintOemUI2::QueryJobAttributes&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui2-queryjobattributes)"><strong>IPrintOemUI2::QueryJobAttributes</strong></a></p></td>
<td><p>允许 UI 插件在调用 <a href="/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvqueryjobattributes" data-raw-source="[&lt;strong&gt;DrvQueryJobAttributes&lt;/strong&gt;](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvqueryjobattributes)"><strong>DrvQueryJobAttributes</strong></a> DDI 后将核心驱动程序的结果后处理。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅 [实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

