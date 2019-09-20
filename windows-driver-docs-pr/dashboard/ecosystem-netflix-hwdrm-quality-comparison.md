---
title: 生态系统 Netflix HWDRM 质量比较
description: 该度量将来自 28 天滑动窗口的遥测数据聚合为二进制值（0 或 1），用于指示驱动程序性能是否在零售市场中来自相同 IHV 的所有驱动程序的聚合性能的 2 个标准差内
ms.topic: article
ms.date: 08/19/2019
ms.localizationpriority: medium
ms.openlocfilehash: c50393db7a49987136ea5bc4366c79c3d4954925
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2019
ms.locfileid: "71017073"
---
# <a name="ecosystem-netflix-hwdrm-quality-comparison"></a>生态系统 Netflix HWDRM 质量比较

## <a name="description"></a>描述

硬件数字版权管理 (HWDRM) 是一项可用于在多个设备平台上安全地播放高清和超高清内容的功能。 此功能可保护数字密钥（如私钥和内容密钥），及压缩和未压缩的视频和音频。 HWDRM 故障会导致用户无法在某些服务（例如 Netflix）上播放视频。 如果驱动程序的会话故障率在零售中来自相同 IHV 的所有驱动程序的平均会话故障率的 2 个标准差内，则通过。  会话故障率较高的那些驱动程序会失败。  

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |生态系统|
|时间段 |28 天滑动窗口|
|度量标准 |实例的聚合|
|最小总体数量 |1 个实例|
|通过标准 |驱动程序会话故障率在所有驱动程序平均会话故障率的 2 个标准差内|
|度量 ID |19170127|

## <a name="calculation"></a>计算

1.  该度量将来自 28 天滑动窗口的遥测数据聚合为二进制值（0 或 1），用于指示驱动程序性能是否在零售市场中来自相同 IHV 的所有驱动程序的聚合性能的 2 个标准差内 

    i.  0 度量结果为成功，表示驱动程序的性能在所有零售驱动程序性能的 95% 内 

2.  评估的驱动程序会话故障率 = 计数（失败会话数）/计数（会话总数） 
3.  零售驱动程序会话故障率 = 计数（失败会话数）/计数（会话总数） 

    i.  对零售市场中来自相同 IHV 的所有其他显卡驱动程序计算一次

4.  零售驱动程序故障率平均值 = 平均值（零售驱动程序会话故障率） 
5.  零售驱动程序故障率标准差 = 标准差（零售驱动程序会话故障率） 
6.  标准差 2 上限 = 平均值 +（零售驱动程序故障率标准差 * 2） 

### <a name="final-calculation"></a>最终计算
8.  Netflix HWDRM 零售比较 =  
    
    i.  如果评估的驱动程序标准故障率 =< 标准偏差 2 上限，则为 0 

    ii. 否则，Netflix HWDRM 零售比较 = 1  

