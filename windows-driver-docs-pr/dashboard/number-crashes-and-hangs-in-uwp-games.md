---
title: 按使用时间规范化的 UWP 游戏中的崩溃和挂起次数（以年为单位）
description: 该度量将 14 天滑动窗口中的遥测数据聚合为未经历内核模式崩溃的计算机所占的百分比
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8a7bc23a5b3191d48942a2ea13a6917ac9e55a89
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2019
ms.locfileid: "71017056"
---
# <a name="number-of-crashes-and-hangs-in-uwp-games-normalized-by-usage-is-less-than-or-equal-to-the-baseline-goal"></a>UWP 游戏中的崩溃和挂起次数（按使用时间规范化）小于或等于基线目标

## <a name="description"></a>描述

当用户玩 UWP 游戏时，显卡组件将处理可视数据，然后在屏幕上显示呈现的视图。 该度量监视 UWP 游戏因显卡组件而崩溃和挂起的频率（相对于这些应用程序在使用该驱动程序的所有设备上的运行时）。 如果应用程序崩溃，则用户可能会丢失进度，并且必须等待该应用程序恢复，然后才能再次使用它。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |生态系统|
|时间段 |7 天滑动窗口|
|度量标准 |实例的聚合|
|最小实例数 |100 小时的 UWP 游戏运行时|
|通过标准 |每年运行时出现 5 次及以下次数的崩溃|
|度量 ID |14842478|

## <a name="calculation"></a>计算

1. 该度量将来自 7 天滑动窗口的遥测数据聚合为 UWP 游戏在运行时（规范化到年）内的崩溃和挂起比率 
2. UWP 游戏的崩溃和挂起总次数 = 计数（使用该驱动程序的每台计算机的 UWP 游戏应用程序的崩溃和挂起次数） 
3. UWP 游戏总运行时 = 总和（使用该驱动程序的每台计算机上的所有 UWP 游戏运行时） 
4. 运行时（年）= UWP 游戏总运行时 \*60（分钟）\*60（小时）\*24（天）\*365（年） 

### <a name="final-calculation"></a>最终计算

按使用时间规范化的 UWP 游戏的崩溃次数 = UWP 游戏的崩溃和挂起总次数/运行时（年）   
