---
title: 创意应用程序中的用户模式可靠性的崩溃次数
description: 了解计算在创意应用程序中发生的崩溃次数的度量值。 该度量值接下来将总运行时规范化为年。
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4bacdf6edf4f336fb38b70a2f6241fbe1c2cc877
ms.sourcegitcommit: cccf9ba62af357aad1016addbbf6c42c7f564412
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2020
ms.locfileid: "91606483"
---
# <a name="number-of-user-mode-reliability-for-crashes-in-creative-applications-normalized-by-usage-is-less-than-or-equal-to-the-baseline-goal"></a>创意应用程序中用户模式可靠性的崩溃次数（按使用时间规范化）小于或等于基线目标

## <a name="description"></a>说明

该度量计算在创意应用程序上下文中发生的显示器驱动程序的崩溃次数，并计算具有更新的驱动程序的所有计算机上的[创意应用程序](measure-appendix.md#creative-applications-example)运行时。 然后，该度量将总运行时规范化到年，指示用户在一年中使用创意应用程序时可能遇到的崩溃次数。

该度量按使用时间规范化，小于或等于基线目标。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众|生态系统|
|时间段|7 天滑动窗口|
|度量标准|实例的聚合|
|最小总体数量|1,000 小时的创意应用程序运行时|
|通过标准|每年运行时出现 10 次及以下次数的崩溃|
|度量 ID |20240835|

## <a name="calculation"></a>计算

1. 该度量将 7 天滑动窗口中的遥测数据聚合为创意应用程序在总运行时（以年为单位）内由显卡驱动程序引起的崩溃比率  。
2. 创意应用程序的崩溃总次数 = 计数（使用该驱动程序的计算机上创意应用程序的崩溃次数） 
3. 创意应用程序总运行时 = 总和（使用该驱动程序的每台计算机的创意应用程序运行时）
4. 运行时（年）= 创意应用程序总运行时 \*60（分钟）\*60（小时）\*24（天）\*365（年）

### <a name="final-calculation"></a>最终计算

按使用时间（年）规范化的创意应用程序的崩溃次数 = 创意应用程序的崩溃总次数/运行时（年）
