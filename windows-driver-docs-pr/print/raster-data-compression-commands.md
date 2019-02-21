---
title: 光栅数据压缩命令
description: 光栅数据压缩命令
ms.assetid: fd88d009-7612-49cc-810a-b0d09b4b75b3
keywords:
- 数据压缩光栅打印命令 WDK Unidrv
- 压缩光栅打印命令 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c61d0cbd6e83971a660d1371d89295be0d11ae66
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522941"
---
# <a name="raster-data-compression-commands"></a>光栅数据压缩命令





下表列出了光栅数据压缩命令。 使用指定的所有命令[命令条目格式](command-entry-format.md)。

有关光栅数据压缩命令的详细信息，请参阅[压缩光栅数据](compressing-raster-data.md)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>命令</th>
<th>描述</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CmdDisableCompression</p></td>
<td><p>命令，以禁用打印机&#39;s 接受所有压缩的数据类型。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="even">
<td><p>CmdEnableDRC</p></td>
<td><p>若要启用打印机的命令&#39;s 接受金压缩的数据。</p></td>
<td><p>可选。 如果未指定，Unidrv 不使用增量行压缩。</p></td>
</tr>
<tr class="odd">
<td><p>CmdEnableFE_RLE</p></td>
<td><p>若要启用打印机的命令&#39;s 接受 FE RLE 压缩的数据。</p></td>
<td><p>可选。 如果未指定，Unidrv 不使用 FE RLE 压缩。</p></td>
</tr>
<tr class="even">
<td><p>CmdEnableOEMComp</p></td>
<td><p>若要启用打印机的命令&#39;s 接受自定义压缩的数据类型。</p></td>
<td><p>可选。 如果未指定，Unidrv 不使用自定义的数据压缩。</p></td>
</tr>
<tr class="odd">
<td><p>CmdEnableTIFF4</p></td>
<td><p>若要启用打印机的命令&#39;s 接受 TIFF 4.0 压缩的数据。</p></td>
<td><p>可选。 如果未指定，Unidrv 不使用 TIFF4.0 压缩。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

 

 




