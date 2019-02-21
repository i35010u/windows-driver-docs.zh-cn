---
title: 捕获视频
description: 捕获视频
ms.assetid: 0adea8fe-1669-4daf-a858-05e014f00a72
keywords:
- 视频捕获 WDK AVStream，捕获进程
- 捕获视频 WDK AVStream，捕获进程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95a6e812fa232d2a6f8f25040e32aadb5c7274ad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546761"
---
# <a name="capturing-video"></a>捕获视频


一旦该流位于**KSSTATE\_运行**状态中时，捕获进程开始。 基于指定的帧间隔**AvgTimePerFrame**的成员[ **KS\_VIDEOINFOHEADER** ](https://msdn.microsoft.com/library/windows/hardware/ff567700)时打开流时，传递的结构流将映像传输到缓冲区通过 SRB\_读取\_数据。 有关捕获映像的其他信息中返回[ **KS\_帧\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567645)追加到末尾的结构[ **KSSTREAM\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff567138)结构。

下面的代码示例获取追加的 KS\_帧\_信息结构：

```cpp
PKSSTREAM_HEADER pDataPacket = pSrb->CommandData.DataBufferArray;
PKS_FRAME_INFO pFrameInfo = (PKS_FRAME_INFO) (pDataPacket + 1); 
```

微型驱动程序应设置捕获帧捕获，丢帧数，例如的数据有关的其他信息字段和字段极性。 帧信息通常存储在驱动程序编写器定义流扩展的成员。

```cpp
*pFrameInfo = pStrmEx->FrameInfo; // Get the frame info from the minidriver-defined stream extension
```

它是更新的最佳**PictureNumber**或**DropCount**的成员[ **KS\_帧\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567645)，[ **KS\_VBI\_帧\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567694)，或[ **KSPROPERTY\_DROPPEDFRAMES\_当前\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565138)在过渡到**KSSTATE\_ACQUIRE**状态。

它是可接受更新这些成员上从过渡**KSSTATE\_ACQUIRE**到状态**KSSTATE\_暂停**状态。

不会更新**PictureNumber**或**DropCount**上从过渡**KSSTATE\_暂停**状态变为**KSSTATE\_运行**状态或**KSSTATE\_运行**状态变为**KSSTATE\_暂停**状态。

如果以前已删除的帧，微型驱动程序应设置中断标志和，然后重设其内部的标志。 下面的代码演示如何设置数据的不连续性标志：

```cpp
if (pStrmEx->fDiscontinuity) {
    pDataPacket->OptionsFlags |= KSSTREAM_HEADER_OPTIONSF_DATADISCONTINUITY;
    pStrmEx->fDiscontinuity = FALSE;
}
```

最后，微型驱动程序应放弃控制 SRB，完成帧捕获。

```cpp
CompleteStreamSRB (pSrb);
```
