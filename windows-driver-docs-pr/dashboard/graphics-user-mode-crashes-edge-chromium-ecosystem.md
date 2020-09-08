---
title: 按使用时间规范化的 Microsoft Edge Chromium 中的用户模式崩溃次数小于等于基线目标（生态系统）
description: 该度量将 7 天滑动窗口中的遥测数据聚合成为 Microsoft Edge Chromium 在总运行时（以年为单位）内由显卡驱动程序引起的崩溃比率（生态系统）
ms.topic: article
ms.date: 05/11/2020
ms.localizationpriority: medium
ms.openlocfilehash: c44d1246087c636a4cb39d506193579e3dab4ccc
ms.sourcegitcommit: 4f08f5686c0bbc27d58930b993cbab1a98e3afb0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89443907"
---
# <a name="number-of-user-mode-crashes-in-microsoft-edge-chromium-normalized-by-usage--baseline-goal-ecosystem"></a>按使用时间规范化的 Microsoft Edge Chromium 中的用户模式崩溃次数小于等于基线目标（生态系统）

## <a name="description"></a>描述

当用户通过 Microsoft Edge Chromium 浏览 Internet 时，显卡组件将处理来自 Web 的可视数据，并在用户屏幕上显示呈现的视图。 该度量监视 Microsoft Edge Chromium 由于显卡驱动程序而崩溃的频率（相对于使用驱动程序的所有设备上的 Microsoft Edge Chromium 运行时）。 如果 Microsoft Edge Chromium 崩溃，用户必须先等待该应用程序恢复，然后才能再次使用它。  

对于[按使用时间规范化的 Microsoft Edge Chromium 中的用户模式崩溃次数小于等于基线目标](./graphics-user-mode-crashes-edge-chromium-standard.md)这一度量，这是它在生态系统中的对应项。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众|生态系统|
|时间段|7 天滑动窗口|
|度量标准|实例的聚合|
|最小总体数量|30,000 小时的 Microsoft Edge Chromium 运行时|
|通过标准|每年崩溃次数小于等于 1|
|度量 ID|25481659|

## <a name="calculation"></a>计算

该度量将 7 天滑动窗口中的遥测数据聚合为 Microsoft Edge Chromium 在总运行时（以年为单位）内由显卡驱动程序引起的崩溃比率

Microsoft Edge Chromium 崩溃总次数 = 计数（Microsoft Edge Chromium 在具有驱动程序的计算机上的崩溃次数）

Microsoft Edge Chromium 总运行时 = 总和（具有驱动程序的每台计算机的 Microsoft Edge Chromium 运行时）

运行时（以年为单位）= Microsoft Edge Chromium 总运行时 ∗ 60（分钟）∗ 60（小时）∗ 24（天）∗ 365（年）

### <a name="final-calculation"></a>最终计算

按使用时间规范化的 Microsoft Edge Chromium 的崩溃次数 = Microsoft Edge Chromium 崩溃总次数/运行时（年）
