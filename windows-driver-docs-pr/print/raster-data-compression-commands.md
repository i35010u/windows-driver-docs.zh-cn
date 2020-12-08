---
title: 光栅数据压缩命令
description: 光栅数据压缩命令
keywords:
- 数据压缩光栅打印命令 WDK Unidrv
- 压缩光栅打印命令 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0cfcf9580b5fe490615f1b6754f96e144dd2129
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807097"
---
# <a name="raster-data-compression-commands"></a>光栅数据压缩命令





下表列出了光栅数据压缩命令。 所有命令都使用 [命令条目格式](command-entry-format.md)指定。

有关光栅数据压缩命令的详细信息，请参阅 [压缩光栅数据](compressing-raster-data.md)。

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
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CmdDisableCompression</p></td>
<td><p>命令来禁用打印机对所有压缩数据类型的接受。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="even">
<td><p>CmdEnableDRC</p></td>
<td><p>命令，用于启用打印机对已进行金压缩的数据的接受。</p></td>
<td><p>可选。 如果未指定，则 Unidrv 不使用 Delta-Row 压缩。</p></td>
</tr>
<tr class="odd">
<td><p>CmdEnableFE_RLE</p></td>
<td><p>命令，用于启用打印机接受 FE-RLE 压缩的数据。</p></td>
<td><p>可选。 如果未指定，则 Unidrv 不使用 FE-RLE 压缩。</p></td>
</tr>
<tr class="even">
<td><p>CmdEnableOEMComp</p></td>
<td><p>用于启用打印机接受自定义压缩数据类型的命令。</p></td>
<td><p>可选。 如果未指定，Unidrv 不会使用自定义的数据压缩。</p></td>
</tr>
<tr class="odd">
<td><p>CmdEnableTIFF4</p></td>
<td><p>命令来启用打印机对 TIFF 4.0 压缩数据的接受。</p></td>
<td><p>可选。 如果未指定，则 Unidrv 不使用 TIFF 4.0 压缩。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

 

 




