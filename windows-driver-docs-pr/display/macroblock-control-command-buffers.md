---
title: 宏块控制命令缓冲区
description: 宏块控制命令缓冲区
ms.assetid: ed6905f6-7e7c-47d2-8f6e-95cfa03e21cb
keywords:
- 宏块 WDK DirectX va，因此命令缓冲区
- 命令缓冲区 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8674be88550a4d13cc8559e44f9f2137634410a8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375396"
---
# <a name="macroblock-control-command-buffers"></a>宏块控制命令缓冲区


## <span id="ddk_macroblock_control_command_buffers_gg"></span><span id="DDK_MACROBLOCK_CONTROL_COMMAND_BUFFERS_GG"></span>


已解码的图片包含一个或多个宏块控制命令缓冲区 （如果它不包含位流缓冲区）。 每个宏块的解码过程中的宏块控制命令缓冲区 （仅一次） 指定。

对于每个宏块控制命令缓冲区，是包含一组相同的块效应的数据的相应残留差异块数据缓冲区。 如果一个或多个[消除马赛克功能筛选器控制缓冲区](deblocking-filter-commands.md)发送，每个 deblocking 的筛选器控制缓冲区中的宏块的一等同于在相应的宏块控制和剩余差异块的块效应的集数据缓冲区。

图片的处理要求每个宏块的运动预测之前添加的残留的差异数据。 可以在以下两种方式之一完成图片解码：

-   宏块控制命令中的动作预测命令缓冲区第一个，然后读取经过运动补偿预测数据重新压缩的目标面上，从处理剩余的差异数据缓冲区时的过程。

-   宏块控制命令缓冲区和残差差异数据缓冲区以协调的方式处理。 将添加到未压缩的目标面写入结果之前，预测的残留的差异数据缓冲区中指定的残留数据。

宏块控制命令和每个宏块的残留的差异数据会影响仅该宏块内的矩形区域。

指定的宏块控制命令缓冲区中的宏块控制命令总数**dwNumMBsInBuffer**的相应成员[ **DXVA\_BufferDescription** ](https://msdn.microsoft.com/library/windows/hardware/ff563122)结构。

数量和类型的残留的差异数据缓冲区中的数据由**wPatternCode**，**全球合作伙伴大会\_Overflow**，并且**bNumCoef**的成员相应的宏块控制命令。

下图显示了宏块控制命令缓冲区和残差差异数据缓冲区之间的关系。

![说明宏块控制命令缓冲区和残差差异数据缓冲区之间的关系的关系图](images/residdiffdata.png)

如果**bConfigMBcontrolRasterOrder**的成员[ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)结构等于 1，则以下表达式所应用到上图中位置*我*是宏块控制命令缓冲区内宏块的索引。

![说明 mb 控制命令缓冲区和残差差异数据缓冲区之间的关系的关系图](images/formula3.png)

 

 





