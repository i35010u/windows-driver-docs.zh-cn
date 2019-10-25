---
title: 捕获视频
description: 捕获视频
ms.assetid: 0adea8fe-1669-4daf-a858-05e014f00a72
keywords:
- 视频捕获 WDK AVStream，捕获过程
- 捕获视频 WDK AVStream，捕获过程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a52ea2a72df32566b529b5d4fbe9303c68ec355a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844736"
---
# <a name="capturing-video"></a>捕获视频


流处于**KSSTATE\_运行**状态后，捕获进程就会开始。 根据在打开流时传递的[**KS\_VIDEOINFOHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_videoinfoheader)结构的**AvgTimePerFrame**成员指定的帧间隔，流将图像传输到通过 SRB\_读取\_数据传递的缓冲区中。 有关捕获的映像的附加信息将在[**KS\_帧\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info)结构中返回，该结构追加到[**KSSTREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)结构的末尾。

下面的示例代码获取追加的 KS\_帧\_信息结构：

```cpp
PKSSTREAM_HEADER pDataPacket = pSrb->CommandData.DataBufferArray;
PKS_FRAME_INFO pFrameInfo = (PKS_FRAME_INFO) (pDataPacket + 1); 
```

微型驱动程序应设置有关捕获的数据的其他信息字段，例如捕获的帧、丢弃的帧以及字段极性。 帧信息通常存储在驱动程序编写器定义的流扩展的成员中。

```cpp
*pFrameInfo = pStrmEx->FrameInfo; // Get the frame info from the minidriver-defined stream extension
```

最佳做法是，更新 Ks\_的**PictureNumber**或**DROPCOUNT**成员[ **\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info)， [**ks\_VBI\_帧\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_vbi_frame_info)或[**KSPROPERTY\_DROPPEDFRAMES\_当前\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_droppedframes_current_s)转换为**KSSTATE\_获取**状态。

在从**KSSTATE\_获取**状态转换为**KSSTATE\_暂停**状态时，可以接受将这些成员更新为可接受的。

请勿将**PictureNumber**或**DropCount**从**KSSTATE\_暂停**状态更新为**KSSTATE\_运行**状态，或者在 KSSTATE **\_运行**状态转换为**KSSTATE\_暂停**状态。

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
