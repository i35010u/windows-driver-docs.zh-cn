---
title: Win32 游戏中的崩溃和挂起次数
description: 该度量将来自 7 天滑动窗口的遥测数据聚合为 Win32 游戏在运行时内的崩溃和挂起比率。
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4abe4352bf55da2b31992bf3ba87563185185761
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "71016981"
---
# <a name="number-of-crashes-and-hangs-in-win32-games-normalized-by-usage-is-less-than-or-equal-to-the-baseline-goal"></a>Win32 游戏中的崩溃和挂起次数（按使用时间规范化）小于或等于基线目标

## <a name="description"></a>说明

当用户玩 Win32 游戏时，显卡组件将处理可视数据，然后在屏幕上显示呈现的视图。 该度量监视 Win32 游戏因显卡组件而崩溃和挂起的频率（相对于这些应用程序在使用该驱动程序的所有设备上的运行时）。 如果应用程序崩溃，则用户可能会丢失进度，并且必须等待该应用程序恢复，然后才能再次使用它。

该度量按使用时间规范化（以年为单位）。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |生态系统|
|时间段 |7 天滑动窗口|
|度量标准 |实例的聚合|
|最小实例数 |100 小时的 Win32 游戏运行时|
|通过标准 |每年运行时出现 5 次及以下次数的崩溃|
|度量 ID |14842479|

## <a name="calculation"></a>计算

1. 该度量将来自 7 天滑动窗口的遥测数据聚合为 Win32 游戏在运行时内的崩溃和挂起比率  。
2. Win32 游戏的崩溃和挂起总次数 = 计数（使用该驱动程序的每台计算机的 Win32 游戏应用程序的崩溃和挂起次数） 
3. Win32 游戏总运行时 = 总和（使用该驱动程序的每台计算机上的所有 Win32 游戏运行时） 
4. 运行时（年）= Win32 游戏总运行时 \*60（分钟）\*60（小时）\*24（天）\*365（年） 

### <a name="final-calculation"></a>最终计算

按使用时间规范化的 Win32 游戏的崩溃次数 = Win32 游戏的崩溃和挂起总次数/运行时（年） 
