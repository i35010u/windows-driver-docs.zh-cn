---
title: Netflix 上的 SWDRM 播放失败次数百分比
description: 该度量将来自 90 天滑动窗口的遥测数据聚合为视频服务中的 SWDRM 播放错误百分比
ms.topic: article
ms.date: 12/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: d554310e46af4968dc104be366ce4728249cb3bf
ms.sourcegitcommit: 90faff267098e5ff04e3c4ffdb63447f2f97df50
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2020
ms.locfileid: "75737321"
---
# <a name="percent-of-swdrm-playback-failures-on-netflix"></a>Netflix 上的 SWDRM 播放失败次数百分比

## <a name="description"></a>说明

软件数字版权管理 (SWDRM) 这项功能使内容分配者能够控制内容的使用方式。 此功能可保护数字密钥（如私钥和内容密钥），及解密的压缩和未压缩的视频。 SWDRM 故障会导致用户无法在某些服务（例如 Netflix）上播放视频。  会话失败率小于或等于 1% 的驱动程序将会通过。 会话故障率较高的那些驱动程序会失败。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |生态系统|
|时间段 |90 天滑动窗口|
|度量标准 |会话实例的聚合|
|最小实例数 |25 个设备|
|通过标准 |驱动程序会话失败率小于或等于 1.0|
|度量 ID |19170139|

## <a name="calculation"></a>计算

1.  输入：90 天的 SWDRM 播放结果，来自 Media Foundation 遥测数据。  此遥测数据会告诉 Microsoft，DRM 视频播放尝试是会导致错误（播放失败）还是不会导致错误（播放成功）。 
2.  以下筛选器用于生成可供度量的干净且可信的数据集： 
    *   仅限零售版，以及最新的预览体验 OS（筛入）
        *   删除 vnext + + OS 将消除来自 OS 的潜在不稳定性
    *   仅限 Netflix 应用和 Edge 中的 Netflix（筛入）
        *   删除其他服务将消除来自其他服务的潜在不稳定性 
    *   预生产设备（筛出）
        *   删除可能无效的设备配置 
    *   仅具有一个 GPU 的设备（筛出）
        *   确保仅分别度量每个 IHV 的结果。 
3.  此外，还会根据以下指标标识并筛出无关设备。  这将删除可能会在用于度量的最终数据集中扭曲结果（正向或负向）的设备。  如果设备的指标结果在指定的百分位标准范围内，则会筛出该设备： 
    *   90 天内每个设备的会话计数：> = 第 95 个百分位
    *   90 天内存在会话的天数：> = 第 97.5 个百分位
    *   90 天内存在会话的每一天的平均会话数：> = 第 97.5 个百分位
    *   90 天内设备上所有会话的失败率：> = 第 95 个百分位


### <a name="final-calculation"></a>最终计算

 失败率 = 100.0 * 计数（失败的会话）/计数（会话总数）
