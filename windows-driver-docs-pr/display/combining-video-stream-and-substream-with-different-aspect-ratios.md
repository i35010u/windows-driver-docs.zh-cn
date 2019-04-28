---
title: 将纵横比不同的视频流和子流合并
description: 本主题说明如何使用不同的纵横比组合的视频流、 视频子流和背景色。
ms.assetid: 3c147829-c76a-4bc7-bb14-bb49609f53d8
keywords:
- 将流和子流 WDK DirectX VA 相结合
- 视频流，以及子流结合使用 WDK DirectX VA
- 子流和视频流结合使用 WDK DirectX VA
- 纵横比 WDK DirectX VA
- 流结合使用 WDK DirectX VA
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: f58bb5a966f7bf6f69cabaffb2e3d72400145eaa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343048"
---
# <a name="combining-video-stream-and-substream-with-different-aspect-ratios"></a>将视频 Stream 和使用不同的纵横比的子流相结合


## <span id="ddk_combining_video_stream_and_substream_with_different_aspect_ratios_"></span><span id="DDK_COMBINING_VIDEO_STREAM_AND_SUBSTREAM_WITH_DIFFERENT_ASPECT_RATIOS_"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。

在以下示例中，VMR 调用驱动程序和不完全涵盖目标表面的视频流目标矩形。 当 VMR 显示 DVD 内容的视频流为 4:3 纵横比，子画面流中 16:9 纵横比，会发生此示例。

下图显示了如何操作，请在此示例中，视频流、 视频子流和背景色组合在一起。

![说明将视频流、 视频子流和背景色组合使用不同的纵横比的关系图](images/trgrect2.png)

在上述示例中，矩形如下所示：

-   对于视频流中，源矩形是 {0，0,720,480} 和目标矩形是 {107，0，747,480}。

-   对于子画面流中，源矩形是 {0，0,720,480} 和目标矩形是 {0，0,854,480}。

-   将目标矩形也是 {0，0,854,480}。

如前面的示例中所示，目标面左侧和右侧边缘包含没有像素从视频流。 在驱动程序**DeinterlaceBltEx**函数应将解释为位于以外的其他视频流的目标矩形作为后台颜色，因为它们合并在一起的子画面流中的像素的像素为单位。

 

 





