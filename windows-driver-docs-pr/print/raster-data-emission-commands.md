---
title: 光栅数据发出命令
description: 光栅数据发出命令
ms.assetid: 31a25de3-f66b-4cf0-90ea-988d75838f68
keywords:
- 数据发出光栅打印命令 WDK Unidrv
- 发出光栅打印命令 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd12851f90f20be054259775302005204fe20981
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521889"
---
# <a name="raster-data-emission-commands"></a>光栅数据发出命令





下表列出了光栅数据发出命令。 使用指定的所有命令[命令条目格式](command-entry-format.md)。

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
<td><p>CmdBeginRaster</p></td>
<td><p>若要初始化光栅数据传输的命令。</p></td>
<td><p>可选。 如果未指定，Unidrv 假定没有初始化所需。</p></td>
</tr>
<tr class="even">
<td><p>CmdEndRaster</p></td>
<td><p>命令完成光栅数据传输。</p></td>
<td><p>可选。 如果未指定，Unidrv 假定任何传输完成操作所需。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSetDestBmpHeight</p></td>
<td><p>若要设置的目标位图的高度的命令。</p></td>
<td><p>可选。 仅在打印机支持可缩放位图时适用。</p></td>
</tr>
<tr class="even">
<td><p>CmdSetDestBmpWidth</p></td>
<td><p>若要设置目标位图的宽度的命令。</p></td>
<td><p>可选。 仅在打印机支持可缩放位图时适用。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSetSrcBmpHeight</p></td>
<td><p>若要设置的源位图的高度的命令。</p></td>
<td><p>可选。 仅在打印机支持可缩放位图时适用。</p></td>
</tr>
<tr class="even">
<td><p>CmdSetSrcBmpWidth</p></td>
<td><p>若要将源位图的宽度设置的命令。</p></td>
<td><p>可选。 仅在打印机支持可缩放位图时适用。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSendBlockData</p></td>
<td><p>若要将数据块传递到打印机的命令。</p></td>
<td><p>必需。 如果 * OutputDataFormat V_BYTE，块包含一个物理打印头传递的数据。 (请参阅 * PinsPerPhysPass)。 如果 *<strong>OutputDataFormat</strong>是 H_BYTE，块包含一个逻辑打印头传递的数据。 (请参阅 * PinsPerLogPass)。</p></td>
</tr>
<tr class="even">
<td><p>CmdEndBlockData</p></td>
<td><p>若要指示使用 CmdSendBlockData 命令发送的数据块的结尾的命令。</p></td>
<td><p>可选。 如果未指定，Unidrv 假定没有命令需要指出的块的末尾。 （由某些点阵打印机。）</p></td>
</tr>
<tr class="odd">
<td><p>CmdSendBlackData</p></td>
<td><p>黑色平面数据传送到打印机的命令。</p></td>
<td><p>如果使用 *<strong>UseExpColorSelectCmd？</strong>属性是<strong>FALSE</strong>。</p></td>
</tr>
<tr class="even">
<td><p>CmdSendBlueData</p></td>
<td><p>蓝色平面数据传送到打印机的命令。</p></td>
<td><p>如果使用 *<strong>UseExpColorSelectCmd？</strong>属性是<strong>FALSE</strong>。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSendCyanData</p></td>
<td><p>青色平面数据传送到打印机的命令。</p></td>
<td><p>如果使用 *<strong>UseExpColorSelectCmd？</strong>属性是<strong>FALSE</strong>。</p></td>
</tr>
<tr class="even">
<td><p>CmdSendGreenData</p></td>
<td><p>绿色平面数据传送到打印机的命令。</p></td>
<td><p>如果使用 *<strong>UseExpColorSelectCmd？</strong>属性是<strong>FALSE</strong>。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSendMagentaData</p></td>
<td><p>洋红色平面数据传送到打印机的命令。</p></td>
<td><p>如果使用 *<strong>UseExpColorSelectCmd？</strong>属性是<strong>FALSE</strong>。</p></td>
</tr>
<tr class="even">
<td><p>CmdSendRedData</p></td>
<td><p>红色平面数据传送到打印机的命令。</p></td>
<td><p>如果使用 * UseExpColorSelectCmd？属性是<strong>FALSE</strong>。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSendYellowData</p></td>
<td><p>黄色平面数据传送到打印机的命令。</p></td>
<td><p>如果使用 *<strong>UseExpColorSelectCmd？</strong>属性是<strong>FALSE</strong>。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

 

 




