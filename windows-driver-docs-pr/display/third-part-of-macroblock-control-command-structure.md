---
title: 宏块控制命令结构的第三部分
description: 宏块控制命令结构的第三部分
ms.assetid: 4e378d2f-dbb2-42b6-984e-b231bb806a7c
keywords:
- 宏块 WDK DirectX VA，通用命令结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d55c8f7824de90007579792eb04254b78fe3a5e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384582"
---
# <a name="third-part-of-macroblock-control-command-structure"></a>宏块控制命令结构的第三部分


## <span id="ddk_third_part_of_macroblock_control_command_structure_gg"></span><span id="DDK_THIRD_PART_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURE_GG"></span>


如果**bPicIntra**的成员[ **DXVA\_PictureParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_pictureparameters)为 1，宏块控制命令结构以结尾中所述的数据[第二个宏块控制命令结构的一部分](second-part-of-macroblock-control-command-structure.md)。 如果**bPicIntra**为零，宏块控制命令来控制运动补偿过程中包含元素的以下附加数据。 之后的数据是一个数组[ **DXVA\_MVvalue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_mvvalue)结构中包含**MVector**宏块控制命令结构的成员。 中的元素数**MVector**图片的 DXVA 成员由指定的类型决定\_PictureParameters 下表中的。

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

 

**请注意**  运动向量中指定数**MVector**宏块的数组控制中定义的命令结构*dxva.h*文件为 4，因为这是最常使用的结构的形式。

 

 

 





