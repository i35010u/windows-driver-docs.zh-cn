---
title: 显示 4 3 中的 16 9 视频目标图面
description: 显示 4 3 中的 16 9 视频目标图面
ms.assetid: 8500ec9c-876d-4b94-a58a-2513942305db
keywords:
- 显示 16 9 视频
- 4 3 个目标面显示 16 9 视频 WDK DirectX VA
- 16 9 视频 4 3 上目标面 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e31f9d83928a71628828d6e6416beccd4cf421e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354735"
---
# <a name="displaying-169-video-within-a-43-destination-surface"></a>在 4:3 目标图面中显示 16:9 视频


## <span id="ddk_displaying_16_9_video_within_a_4_3_destination_surface_gg"></span><span id="DDK_DISPLAYING_16_9_VIDEO_WITHIN_A_4_3_DESTINATION_SURFACE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。

在以下示例中，VMR 指示要显示 4:3 目标面中的 16:9 视频流。

![说明 16:9 视频 4:3 目标面中的关系图](images/trgrect.png)

请注意，为了清楚起见前面的示例中不包含任何视频子流。 在上述示例中，矩形如下所示：

-   目标矩形 = {0，0，640，480}

-   视频流：
    -   源矩形 = {0，0、 720、 480}
    -   目标矩形 = {0，60,640,300}

 

 





