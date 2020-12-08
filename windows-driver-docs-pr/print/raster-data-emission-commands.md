---
title: 光栅数据发射命令
description: 光栅数据发射命令
keywords:
- 数据发射光栅打印命令 WDK Unidrv
- 发射光栅打印命令 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcb04525f7669a47495d5047bb0a8376cd517be3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807087"
---
# <a name="raster-data-emission-commands"></a>光栅数据发射命令





下表列出了光栅数据发射命令。 所有命令都使用 [命令条目格式](command-entry-format.md)指定。

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
<td><p>CmdBeginRaster</p></td>
<td><p>用于初始化光栅数据传输的命令。</p></td>
<td><p>可选。 如果未指定，则 Unidrv 假定不需要初始化。</p></td>
</tr>
<tr class="even">
<td><p>CmdEndRaster</p></td>
<td><p>用于完成光栅数据传输的命令。</p></td>
<td><p>可选。 如果未指定，则 Unidrv 假定不需要传输完成操作。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSetDestBmpHeight</p></td>
<td><p>命令设置目标位图的高度。</p></td>
<td><p>可选。 仅当打印机支持可缩放的位图时才适用。</p></td>
</tr>
<tr class="even">
<td><p>CmdSetDestBmpWidth</p></td>
<td><p>命令设置目标位图的宽度。</p></td>
<td><p>可选。 仅当打印机支持可缩放的位图时才适用。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSetSrcBmpHeight</p></td>
<td><p>命令设置源位图的高度。</p></td>
<td><p>可选。 仅当打印机支持可缩放的位图时才适用。</p></td>
</tr>
<tr class="even">
<td><p>CmdSetSrcBmpWidth</p></td>
<td><p>用于设置源位图宽度的命令。</p></td>
<td><p>可选。 仅当打印机支持可缩放的位图时才适用。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSendBlockData</p></td>
<td><p>用于将数据块传递到打印机的命令。</p></td>
<td><p>必需。 如果 V_BYTE * OutputDataFormat，则块包含打印头的一次物理轮的数据。  (参阅 * PinsPerPhysPass) 。 如果 H_BYTE *<strong>OutputDataFormat</strong> ，则块包含打印头的一个逻辑处理过程的数据。  (参阅 * PinsPerLogPass) 。</p></td>
</tr>
<tr class="even">
<td><p>CmdEndBlockData</p></td>
<td><p>用于指示已使用 CmdSendBlockData 命令发送的数据块结尾的命令。</p></td>
<td><p>可选。 如果未指定，Unidrv 将假定不需要使用任何命令来指示块的结尾。  (某些点阵打印机使用 ) </p></td>
</tr>
<tr class="odd">
<td><p>CmdSendBlackData</p></td>
<td><p>用于将黑色平面数据传递到打印机的命令。</p></td>
<td><p>如果 *<strong>UseExpColorSelectCmd？</strong> 属性为 <strong>FALSE</strong>，则为必需。</p></td>
</tr>
<tr class="even">
<td><p>CmdSendBlueData</p></td>
<td><p>用于将蓝平面数据传递到打印机的命令。</p></td>
<td><p>如果 *<strong>UseExpColorSelectCmd？</strong> 属性为 <strong>FALSE</strong>，则为必需。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSendCyanData</p></td>
<td><p>用于将青色平面数据传递到打印机的命令。</p></td>
<td><p>如果 *<strong>UseExpColorSelectCmd？</strong> 属性为 <strong>FALSE</strong>，则为必需。</p></td>
</tr>
<tr class="even">
<td><p>CmdSendGreenData</p></td>
<td><p>用于向打印机传递绿色平面数据的命令。</p></td>
<td><p>如果 *<strong>UseExpColorSelectCmd？</strong> 属性为 <strong>FALSE</strong>，则为必需。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSendMagentaData</p></td>
<td><p>用于向打印机传递洋红色平面数据的命令。</p></td>
<td><p>如果 *<strong>UseExpColorSelectCmd？</strong> 属性为 <strong>FALSE</strong>，则为必需。</p></td>
</tr>
<tr class="even">
<td><p>CmdSendRedData</p></td>
<td><p>用于将红色平面数据传递到打印机的命令。</p></td>
<td><p>是否需要 * UseExpColorSelectCmd？属性为 <strong>FALSE</strong>。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSendYellowData</p></td>
<td><p>用于将黄色平面数据传递到打印机的命令。</p></td>
<td><p>如果 *<strong>UseExpColorSelectCmd？</strong> 属性为 <strong>FALSE</strong>，则为必需。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

 

 




