---
title: 宏块控制命令结构的第三部分
description: 宏块控制命令结构的第三部分
ms.assetid: 4e378d2f-dbb2-42b6-984e-b231bb806a7c
keywords:
- macroblocks WDK DirectX VA，通用命令结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b5cc5499631a6902954e74a2ea7497bde1431a6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829327"
---
# <a name="third-part-of-macroblock-control-command-structure"></a>宏块控制命令结构的第三部分


## <span id="ddk_third_part_of_macroblock_control_command_structure_gg"></span><span id="DDK_THIRD_PART_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURE_GG"></span>


如果[**DXVA\_PictureParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)的**bPicIntra**成员为1，则宏块 Control 命令结构以[宏块 Control 命令结构的第二部分](second-part-of-macroblock-control-command-structure.md)所述的数据结尾。 如果**bPicIntra**为零，则宏块控件命令中将包含以下附加数据元素，以控制运动补偿过程。 接下来的数据是[ **\_DXVA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mvvalue)的数组，其中包含**MVector**成员中包含的宏块 Control 命令结构的 MVvalue 结构。 **MVector**中的元素数取决于下表中由 DXVA\_PictureParameters 成员指定的图片类型。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bPicOBMC</th>
<th align="left">bPicBinPB</th>
<th align="left">bPic4MVallowed</th>
<th align="left">MVector 中的元素数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="even">
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="even">
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>11</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>11</p></td>
</tr>
</tbody>
</table>

 

**请注意**   在**MVector**数组中为*dxva*文件中定义的宏块控制命令结构指定的运动矢量数量为四，因为这是最常用的结构形式。

 

 

 





