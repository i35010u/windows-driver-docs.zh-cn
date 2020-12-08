---
title: 捕获视频
description: 捕获视频
keywords:
- 视频捕获 WDK AVStream，捕获过程
- 捕获视频 WDK AVStream，捕获过程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58f9a43b6aa0135034b62d296d72988d64da9ba4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839361"
---
# <a name="capturing-video"></a>捕获视频


流处于 **KSSTATE \_ 运行** 状态后，捕获进程开始。 根据打开流时传递的 [**KS \_ VIDEOINFOHEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_videoinfoheader)结构的 **AvgTimePerFrame** 成员所指定的帧间隔，流将图像传输到通过 SRB 读取数据传递的缓冲区中 \_ \_ 。 有关捕获的映像的附加信息将返回到在 [**KSSTREAM \_ 标头**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)结构末尾追加的 " [**KS \_ 帧 \_ 信息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info)结构" 中。

下面的示例代码获取追加的 KS \_ 帧 \_ 信息结构：

```cpp
PKSSTREAM_HEADER pDataPacket = pSrb->CommandData.DataBufferArray;
PKS_FRAME_INFO pFrameInfo = (PKS_FRAME_INFO) (pDataPacket + 1); 
```

微型驱动程序应设置有关捕获的数据的其他信息字段，例如捕获的帧、丢弃的帧以及字段极性。 帧信息通常存储在驱动程序编写器定义的流扩展的成员中。

```cpp
*pFrameInfo = pStrmEx->FrameInfo; // Get the frame info from the minidriver-defined stream extension
```

最佳做法是，在转换为 **DROPPEDFRAMES \_ 获取** 状态时，更新 [**ks \_ 帧 \_ 信息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info)、 [**ks \_ VBI \_ 帧 \_ 信息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_vbi_frame_info)或 [**KSPROPERTY \_ KSSTATE \_ 当前 \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_droppedframes_current_s)的 **PictureNumber** 或 **DropCount** 成员。

在从 **KSSTATE \_ 获取** 状态转换到 **KSSTATE \_ 暂停** 状态时，可以接受将这些成员更新。

请勿将 **PictureNumber** 或 **DropCount** 从 **KSSTATE \_ 暂停** 状态更新为 **KSSTATE \_ 运行** 状态，或将 **KSSTATE \_ 运行** 状态转换为 **KSSTATE \_ 暂停** 状态。

如果以前删除了帧，则微型驱动程序应设置中断标志，然后重置其内部标志。 下面的代码演示如何设置数据连续性标志：

```cpp
if (pStrmEx->fDiscontinuity) {
    pDataPacket->OptionsFlags |= KSSTREAM_HEADER_OPTIONSF_DATADISCONTINUITY;
    pStrmEx->fDiscontinuity = FALSE;
}
```

最后，微型驱动程序应放弃对 SRB 的控制，完成帧捕获。

```cpp
CompleteStreamSRB (pSrb);
```
