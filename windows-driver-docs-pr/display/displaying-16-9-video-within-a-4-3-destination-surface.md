---
title: 在 4 3 目标图面中显示 16 9 视频
description: 在 4 3 目标图面中显示 16 9 视频
keywords:
- 显示 16 9 视频
- 4 3 目标表面显示 16 9 视频 WDK DirectX VA
- 16 9 4 3 目标图面上的视频-DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e436f03eeed16c00b1324a7a47e51a362ab7176
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809225"
---
# <a name="displaying-169-video-within-a-43-destination-surface"></a>在 4:3 目标图面中显示 16:9 视频


## <span id="ddk_displaying_16_9_video_within_a_4_3_destination_surface_gg"></span><span id="DDK_DISPLAYING_16_9_VIDEO_WITHIN_A_4_3_DESTINATION_SURFACE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

在下面的示例中，VMR 指示在4:3 目标图面中显示16:9 视频流。

![在4:3 目标图面中展示16:9 视频的示意图](images/trgrect.png)

请注意，为清楚起见，前面的示例不包含任何视频 substreams。 在前面的示例中，矩形如下所示：

-   目标矩形 = {0，0，640，480}

-   视频流：
    -   源矩形 = {0，0，720，480}，
    -   目标矩形 = {0，60640300}

 

 





