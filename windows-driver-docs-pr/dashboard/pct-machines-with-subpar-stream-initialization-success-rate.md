---
title: 流初始化成功率低于标准成功率的计算机的百分比
description: 该度量将 7 天滑动窗口中的遥测数据聚合为其初始化率低于标准的计算机所占的百分比
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5c2d0ea92efe7473bc0aee6686180158e624b387
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2019
ms.locfileid: "71017021"
---
# <a name="percent-of-machines-with-subpar-stream-initialization-success-rate"></a>流初始化成功率低于标准成功率的计算机的百分比

## <a name="description"></a>描述

该度量确定每台计算机的初始化成功率，并计算其流初始化率低于 90% 的计算机所占的百分比  。 当设备无法初始化音频流时，用户将无法使用应用程序的音频体验。 

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |Standard|
|时间段 |7 天|
|度量标准 |计算机的聚合|
|最小总体数量 |50 台计算机|
|通过标准 |<= 1 % 的计算机初始化成功率低于 90% |
|度量 ID |11458866|

## <a name="calculation"></a>计算

1. 该度量将 7 天滑动窗口中的遥测数据聚合为初始化率低于标准的计算机所占的百分比  。
2. 对于每台计算机，计算： 

   a. 计算机的初始化成功率 = 计数（失败的初始化次数）/计数（尝试的总初始化次数） 

   b. 失败的计算机 = 计算机的初始化成功率 < 90% 

3. 初始化低于标准的计算机数 = 计数（失败的计算机） 
4. 计算机总数 = 计数（尝试初始化的所有计算机） 

### <a name="final-calculation"></a>最终计算

初始化率低于标准的计算机的百分比 = 初始化低于标准的计算机数/计算机总数 
