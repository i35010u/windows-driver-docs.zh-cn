---
title: 将纵横比不同的视频流和子流合并
description: 本主题说明如何将视频流、视频子流和背景色与不同纵横比结合在一起。
keywords:
- 合并流和子流 WDK DirectX VA
- 视频流和子流组合 WDK DirectX VA
- 子流和视频流组合 WDK DirectX VA
- 纵横比 WDK DirectX VA
- 流组合 WDK DirectX VA
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 8039f4d116efaf0b6805584895bf1344b2d4f5b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810271"
---
# <a name="combining-video-stream-and-substream-with-different-aspect-ratios"></a>结合不同纵横比的视频流和子流


## <span id="ddk_combining_video_stream_and_substream_with_different_aspect_ratios_"></span><span id="DDK_COMBINING_VIDEO_STREAM_AND_SUBSTREAM_WITH_DIFFERENT_ASPECT_RATIOS_"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

在下面的示例中，VMR 使用未完全涵盖目标图面的视频流目标矩形调用驱动程序。 如果 VMR 显示的 DVD 内容的视频流处于4:3 纵横比，并且子画面流处于16:9 纵横比，则会出现此示例。

下图显示了在此示例中，如何合并视频流、视频子流和背景色。

![说明如何将视频流、视频子流和背景色与不同纵横比合并的关系图](images/trgrect2.png)

在前面的示例中，矩形如下所示：

-   对于视频流，源矩形为 {0，0720480}，目标矩形为 {107，0，747480}。

-   对于子画面流，源矩形为 {0，0720480}，目标矩形为 {0，0854480}。

-   目标矩形也是 {0，0854480}。

如前面的示例所示，目标图面的左边缘和右边缘不包含视频流中的任何像素。 驱动程序的 **DeinterlaceBltEx** 函数应将位于视频流的目标矩形之外的像素解释为 backgound 颜色，因为它们与子画面流中的像素合并在一起。

 

 





