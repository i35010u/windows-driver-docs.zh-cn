---
title: 宏块控制命令缓冲区
description: 宏块控制命令缓冲区
ms.assetid: ed6905f6-7e7c-47d2-8f6e-95cfa03e21cb
keywords:
- macroblocks WDK DirectX VA，命令缓冲区
- 命令缓冲区 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c4a9266047af1af3425a1daa87e7a2f9bcf4962
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065754"
---
# <a name="macroblock-control-command-buffers"></a>宏块控制命令缓冲区


## <span id="ddk_macroblock_control_command_buffers_gg"></span><span id="DDK_MACROBLOCK_CONTROL_COMMAND_BUFFERS_GG"></span>


解码图片包含一个或多个宏块控制命令缓冲区 (如果它不包含位流缓冲区) 。 每个宏块的解码过程指定 (仅) 在宏块控件命令缓冲区中。

对于每个宏块控件命令缓冲区，都有一个对应的残留差异块数据缓冲区，其中包含同一组 macroblocks 的数据。 如果发送一个或多个 [deblocking 筛选器控件缓冲区](deblocking-filter-commands.md) ，则每个 deblocking 筛选器控件缓冲区中的 macroblocks 集与相应宏块控件中的一组 macroblocks 和剩余差异块数据缓冲区相同。

图片处理要求每个宏块的运动预测在添加残留差异数据之前。 可以通过以下两种方式之一来完成图片解码：

-   首先处理宏块控件命令缓冲区中的运动预测命令，然后在处理残留差数据缓冲区的过程中从未压缩的目标表面读取返回的运动补偿预测数据。

-   以协调方式处理宏块控件命令缓冲区和残留差异数据缓冲区。 将残留差异数据缓冲区中指定的残留数据添加到预测，然后再将结果写入到未压缩的目标图面。

每个宏块的宏块控制命令和残留差异数据只影响该宏块中的矩形区域。

宏块控件命令缓冲区中的宏块控制命令总数由相应[**DXVA \_ BufferDescription**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_bufferdescription)结构的**dwNumMBsInBuffer**成员指定。

残留差数据缓冲区中数据的数量和类型由相应宏块 control 命令的 **wPatternCode**、 **wPC \_ **和 **bNumCoef** 成员确定。

下图显示了宏块控件命令缓冲区与残留差异数据缓冲区之间的关系。

![说明宏块控件命令缓冲区与残留差异数据缓冲区之间的关系的关系图](images/residdiffdata.png)

如果[**DXVA \_ ConfigPictureDecode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)结构的**bConfigMBcontrolRasterOrder**成员等于1，则以下表达式将应用于上图，其中*i*是宏块控件命令缓冲区内的宏块的索引。

![说明 mb 控制命令缓冲区与残留差异数据缓冲区之间的关系的关系图](images/formula3.png)

 

