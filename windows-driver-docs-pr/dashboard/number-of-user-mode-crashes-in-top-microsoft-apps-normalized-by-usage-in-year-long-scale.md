---
title: 热门 Microsoft 应用中用户模式的崩溃次数（生态系统）
description: 该度量将 7 天滑动窗口中的遥测数据聚合为热门 Microsoft 应用在总运行时（以年为单位）内由显卡驱动程序引起的崩溃比率
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: d2056e030f968784b764a746400fe34539f466e7
ms.sourcegitcommit: b331d736356095f852629402bd1a0becbb396ede
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2020
ms.locfileid: "90765313"
---
# <a name="number-of-user-mode-crashes-in-top-microsoft-apps-normalized-by-usage-is-less-than-or-equal-to-the-baseline-goal-ecosystem"></a>热门 Microsoft 应用中用户模式的崩溃次数（按使用时间规范化）小于或等于基线目标（生态系统）

## <a name="description"></a>描述

当用户打开并使用应用程序时，显卡组件将处理应用的可视信息并在用户屏幕上显示呈现的视图。 该度量监视热门 Microsoft 应用的崩溃频率（相对于这些应用程序在使用该驱动程序的所有设备上的运行时）。 如果应用程序崩溃，用户必须先等待其恢复，然后才能再次使用它。

该度量按使用时间规范化（以年为单位）。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众|生态系统|
|时间段|7 天滑动窗口|
|度量标准|实例的聚合|
|最小总体数量|100,000 小时的热门 Microsoft 应用运行时|
|通过标准|每年运行时出现 1.5 次及以下次数的崩溃|
|度量 ID|17377268|

## <a name="calculation"></a>计算

1. 该度量将 7 天滑动窗口中的遥测数据聚合为热门 Microsoft 应用在总运行时（以年为单位）内由显卡驱动程序引起的崩溃比率。
2. 热门 Microsoft 应用中的崩溃总次数 = 计数（热门 Microsoft 应用在使用该驱动程序的计算机上的崩溃次数）
3. 热门 Microsoft 应用的总运行时 = 总和（使用该驱动程序的每台计算机的热门 Microsoft 应用运行时）
4. 运行时（年）= 热门 Microsoft 应用的总运行时 \*60（分钟）\*60（小时）\*24（天）\*365（年）

### <a name="final-calculation"></a>最终计算

按使用时间规范化的热门 Microsoft 应用的崩溃次数 = 热门 Microsoft 应用中的崩溃总次数/运行时（年）