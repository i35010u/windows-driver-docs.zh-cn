---
title: 宏块控制命令结构的第四部分
description: 宏块控制命令结构的第四部分
keywords:
- macroblocks WDK DirectX VA，通用命令结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68c4ca83019c439e0291127d69c08e38e4fec011
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799685"
---
# <a name="fourth-part-of-macroblock-control-command-structure"></a>宏块控制命令结构的第四部分


## <span id="ddk_fourth_part_of_macroblock_control_command_structure_gg"></span><span id="DDK_FOURTH_PART_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURE_GG"></span>


如果 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)的 **bPicIntra** 和 **bMV \_ RPS** 成员为零，则宏块控件命令结构以 [宏块控件命令结构的第三部分](third-part-of-macroblock-control-command-structure.md)所述的数据结尾。 宏块控件命令结构以使用零值数据填充的结构的第三部分结束（如有必要），以便将下一个宏块控件命令与16字节边界对齐。

如果 DXVA PictureParameters 的 **bPicIntra** 成员 \_ 为零，DXVA PictureParameters 的 **bMV \_ RPS** 成员 \_ 为1，则宏块控件命令结构的第四部分是名为 *bRefPicSelect* 的字节数组。 该数组中的元素数与上表中显示的 **MVector** 数组中的元素数相同。 数组的每个元素指定与在 **MVector** 数组中找到的相应运动向量关联的未压缩图面的索引。 然后，宏块控件命令结构结束并使用零值数据进行填充（如有必要），以便将下一个宏块控件命令结构与16字节边界对齐。

 

