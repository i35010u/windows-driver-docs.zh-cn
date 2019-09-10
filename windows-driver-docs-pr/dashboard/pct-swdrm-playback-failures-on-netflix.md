---
title: Netflix 上的 SWDRM 播放失败次数百分比
description: 该度量将来自 7 天滑动窗口的遥测数据聚合为 Netflix 中的 SWDRM 播放错误百分比
ms.topic: article
ms.date: 05/20/2019
ms.author: paslote
author: parkeratmicrosoft
ms.localizationpriority: medium
ms.openlocfilehash: 1a511c70b66300003c74cfc0dd92d7af1446ef59
ms.sourcegitcommit: 04da1962e34908adeca54fcf5bbfbaa456efca5f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2019
ms.locfileid: "70223913"
---
# <a name="percent-of-swdrm-playback-failures-on-netflix"></a>Netflix 上的 SWDRM 播放失败次数百分比

## <a name="description"></a>描述

软件数字版权管理 (SWDRM) 这项功能使内容分配者能够控制内容的使用方式。 此功能可保护数字密钥（如私钥和内容密钥），及解密的压缩和未压缩的视频。 SWDRM 故障会导致用户无法在某些服务（例如 Netflix）上播放视频。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |生态系统|
|时间段 |7 天滑动窗口|
|度量标准 |实例的聚合|
|最小实例数 |200 次 Netflix 播放|
|通过标准 |<= 1% 的 Netflix 播放出现 SWDRM 故障|
|度量 ID |19170139|

## <a name="calculation"></a>计算

1. 该度量将来自 7 天滑动窗口的遥测数据聚合为 Netflix 中的 SWDRM 播放错误百分比  。

   a. 播放失败 = Netflix 视频上填充有 \<video>.error 元素 

2. Netflix SWDRM 播放失败次数 = 计数（播放失败数） 
3. 总 Netflix 视频数 = 计数（Netflix 上的 \<video> 元素数） 

### <a name="final-calculation"></a>最终计算

SWDRM Netflix 播放错误百分比 = Netflix HWDRM 播放失败次数/总 Netflix 视频数 
