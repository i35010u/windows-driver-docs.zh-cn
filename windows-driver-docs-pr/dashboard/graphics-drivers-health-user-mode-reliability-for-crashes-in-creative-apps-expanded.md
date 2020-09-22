---
title: 创意应用程序中用户模式可靠性的崩溃次数（已扩展）
description: 该度量将 7 天滑动窗口中的遥测数据聚合为创意应用程序在总运行时（以年为单位）内由显卡驱动程序引起的崩溃比率
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: dc21e76c81a26805c8c038df45ead3c575e050c2
ms.sourcegitcommit: b331d736356095f852629402bd1a0becbb396ede
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2020
ms.locfileid: "90765318"
---
# <a name="number-of-user-mode-reliability-for-crashes-in-creative-applications-normalized-by-usage-is-less-than-or-equal-to-the-baseline-goal-expanded"></a>创意应用程序中用户模式可靠性的崩溃次数（按使用时间规范化）小于或等于基线目标（已扩展）

## <a name="description"></a>描述

该度量计算在创意应用程序上下文中发生的显示器驱动程序的崩溃次数，并计算具有更新的驱动程序的所有计算机上的[创意应用程序](measure-appendix.md#creative-applications-example)运行时。 然后，该度量将总运行时规范化到年，指示用户在一年中使用创意应用程序时可能遇到的崩溃次数。

该度量按使用时间规范化，小于或等于基线目标。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众|展开|
|时间段|7 天滑动窗口|
|度量标准|实例的聚合|
|最小总体数量|1,000 小时的创意应用程序运行时|
|通过标准|每年运行时出现 10 次及以下次数的崩溃|
|度量 ID|22843595|

## <a name="calculation"></a>计算

1. 该度量将 7 天滑动窗口中的遥测数据聚合为创意应用程序在总运行时（以年为单位）内由显卡驱动程序引起的崩溃比率。
2. 创意应用程序的崩溃总次数 = 计数（使用该驱动程序的计算机上创意应用程序的崩溃次数）
3. 创意应用程序总运行时 = 总和（使用该驱动程序的每台计算机的创意应用程序运行时）
4. 运行时（年）= 创意应用程序总运行时 \*60（分钟）\*60（小时）\*24（天）\*365（年）

### <a name="final-calculation"></a>最终计算

按使用时间（年）规范化的创意应用程序的崩溃次数 = 创意应用程序的崩溃总次数/运行时（年）
