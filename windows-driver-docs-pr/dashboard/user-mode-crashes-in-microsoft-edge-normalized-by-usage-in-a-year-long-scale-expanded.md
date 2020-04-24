---
title: Microsoft Edge 中的用户模式崩溃次数
description: 该度量将 7 天滑动窗口中的遥测数据聚合为 Microsoft Edge 在总运行时（以年为单位）内由显卡驱动程序引起的崩溃比率
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: c6cf0803e98bc260dc3419170f7dcd4852ddbd8f
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "71017011"
---
# <a name="number-of-user-mode-reliability-for-crashes-in-microsoft-edge-normalized-by-usage-is-less-than-or-equal-to-the-baseline-goal"></a>Microsoft Edge 中用户模式可靠性的崩溃次数（按使用时间规范化）小于或等于基线目标

## <a name="description"></a>说明

当用户通过 Microsoft Edge 浏览 Internet 时，显卡组件将处理来自 Web 的可视数据，并在用户屏幕上显示呈现的视图。 该度量监视 Microsoft Edge 的崩溃频率（相对于使用该驱动程序的所有设备上的 Microsoft Edge 运行时）。 如果 Microsoft Edge 崩溃，用户必须先等待该应用程序恢复，然后才能再次使用它。

该度量按使用时间规范化（以年为单位）。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |展开|
|时间段 |7 天滑动窗口|
|度量标准 |实例的聚合|
|最小总体数量 |30,000 小时的 Microsoft Edge 运行时|
|通过标准 |每年运行时出现 1 次及以下次数的崩溃|
|度量 ID |22728062|

## <a name="calculation"></a>计算

1. 该度量将 7 天滑动窗口中的遥测数据聚合为 Microsoft Edge 在总运行时（以年为单位）内由显卡驱动程序引起的崩溃比率 
2. Microsoft Edge 崩溃总次数 = 计数（Microsoft Edge 在具有该驱动程序的计算机上的崩溃次数） 
3. Microsoft Edge 总运行时 = 总和（具有该驱动程序的每台计算机的 Microsoft Edge 运行时） 
4. 运行时（年）= Microsoft Edge 总运行时 \*60（分钟）\*60（小时）\*24（天）\*365（年） 

### <a name="final-calculation"></a>最终计算

按使用时间规范化的 Microsoft Edge 的崩溃次数 = Microsoft Edge 崩溃总次数/运行时（年） 