---
title: IPrintCorePS2 COM 接口
description: IPrintCorePS2 COM 接口
ms.assetid: d5eb6962-2201-405f-9a22-2b11fb6d0360
keywords:
- IPrintCorePS2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaf75902b774778c684bf18646c1b9ef83c5fb4c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839631"
---
# <a name="iprintcoreps2-com-interface"></a>IPrintCorePS2 COM 接口





`IPrintCorePS2` COM 接口为 Pscript5 render 插件提供一组帮助器方法。下表列出并描述了 `IPrintCorePS2` 接口定义的所有方法。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-drvwritespoolbuf" data-raw-source="[&lt;strong&gt;IPrintCorePS2::DrvWriteSpoolBuf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-drvwritespoolbuf)"><strong>IPrintCorePS2：:D rvWriteSpoolBuf</strong></a></p></td>
<td><p>由 Pscript5 驱动程序提供，以便<a href="rendering-plug-ins.md" data-raw-source="[rendering plug-ins](rendering-plug-ins.md)">呈现插件</a>可以将打印机数据发送到后台处理程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-enumfeatures" data-raw-source="[&lt;strong&gt;IPrintCorePS2::EnumFeatures&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-enumfeatures)"><strong>IPrintCorePS2::EnumFeatures</strong></a></p></td>
<td><p>枚举打印机的可用功能。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-enumoptions" data-raw-source="[&lt;strong&gt;IPrintCorePS2::EnumOptions&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-enumoptions)"><strong>IPrintCorePS2::EnumOptions</strong></a></p></td>
<td><p>枚举特定功能的可用选项。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-getfeatureattribute" data-raw-source="[&lt;strong&gt;IPrintCorePS2::GetFeatureAttribute&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-getfeatureattribute)"><strong>IPrintCorePS2::GetFeatureAttribute</strong></a></p></td>
<td><p>检索功能属性列表或特定功能属性的值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-getglobalattribute" data-raw-source="[&lt;strong&gt;IPrintCorePS2::GetGlobalAttribute&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-getglobalattribute)"><strong>IPrintCorePS2::GetGlobalAttribute</strong></a></p></td>
<td><p>检索全局属性列表或特定全局属性的值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-getoptionattribute" data-raw-source="[&lt;strong&gt;IPrintCorePS2::GetOptionAttribute&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-getoptionattribute)"><strong>IPrintCorePS2::GetOptionAttribute</strong></a></p></td>
<td><p>检索选项属性列表或特定选项属性的值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-getoptions" data-raw-source="[&lt;strong&gt;IPrintCorePS2::GetOptions&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-getoptions)"><strong>IPrintCorePS2::GetOptions</strong></a></p></td>
<td><p>以功能/选项关键字对的列表格式检索驱动程序的当前功能设置。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅[实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 

 




