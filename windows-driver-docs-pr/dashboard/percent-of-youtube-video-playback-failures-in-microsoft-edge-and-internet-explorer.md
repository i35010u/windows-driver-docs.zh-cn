---
title: Microsoft Edge 和 Internet Explorer 中的 YouTube 视频播放失败次数百分比
description: 该度量将来自 7 天滑动窗口的遥测数据聚合为 Microsoft Edge 或 Internet Explorer 中的 YouTube 播放错误百分比
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 74a0af946d837fe120dd6dc7fe34086b661cadab
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2019
ms.locfileid: "71016943"
---
# <a name="percent-of-youtube-video-playback-failures-in-microsoft-edge-and-internet-explorer"></a>Microsoft Edge 和 Internet Explorer 中的 YouTube 视频播放失败次数百分比

## <a name="description"></a>描述

当用户使用 Microsoft Edge 或 Internet Explorer 观看 YouTube 视频时，显卡组件将处理来自 Web 的视频流，并在屏幕上显示呈现的视频。 该度量监视 YouTube 视频在 Microsoft Edge 中播放失败的频率；如果用户遇到播放失败，他们将无法加载和观看视频。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |Standard |
|时间段 |7 天滑动窗口|
|度量标准 |实例的聚合|
|最小实例数 |50 次 YouTube 播放次数|
|通过标准 |<= 1% 的 YouTube 视频元素具有 \<video>.error 属性|
|度量 ID |6195478|

## <a name="calculation"></a>计算

1. 该度量将来自 7 天滑动窗口的遥测数据聚合为 Microsoft Edge 或 Internet Explorer 中的 YouTube 播放错误百分比  。
2. 会话 = 将 YouTube 媒体资源加载到 HTML5 \<video> 元素的单个实例 

   a. 一台计算机可以有多个会话。

3. 播放失败次数 = 计数（Microsoft Edge 或 Internet Explorer 中遇到的 YouTube \<video>.error 元素）

### <a name="final-calculation"></a>最终计算

Microsoft Edge 或 Internet Explorer YouTube HTML5 播放失败的百分比 = 播放失败次数/计数（会话） 
