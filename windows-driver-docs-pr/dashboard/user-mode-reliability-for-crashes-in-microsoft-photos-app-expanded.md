---
title: Microsoft 照片应用中用户模式可靠性的崩溃次数，小于或等于基线目标
description: 该度量将 7 天滑动窗口中的遥测数据聚合为 Microsoft 照片在总运行时（以年为单位）内由显卡驱动程序引起的崩溃比率
ms.topic: article
ms.date: 08/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 762a85c8e3064d200ce7e1f61b932ba1647eedf9
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2019
ms.locfileid: "71016993"
---
# <a name="number-of-user-mode-reliability-for-crashes-in-microsoft-photos-app-normalized-by-usage-is-less-than-or-equal-to-the-baseline-goal"></a>Microsoft 照片应用中用户模式可靠性的崩溃次数（按使用时间规范化）小于或等于基线目标

## <a name="description"></a>描述

该度量计算在 Microsoft 照片应用程序上下文中发生的显示器驱动程序的崩溃次数，并计算具有更新的驱动程序的所有计算机上的 Microsoft 照片运行时。 然后，该度量将总运行时规范化到年，指示用户在一年中使用 Microsoft 照片时可能遇到的崩溃次数。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |展开|
|时间段 |7 天滑动窗口|
|度量标准 |实例的聚合|
|最小实例数 |10,000 小时的 Microsoft 照片运行时 |
|通过标准 |每年运行时出现 1.5 次及以下次数的崩溃|
|度量 ID |22726049|

## <a name="calculation"></a>计算

1. 该度量将 7 天滑动窗口中的遥测数据聚合为 Microsoft 照片在总运行时（以年为单位）内由显卡驱动程序引起的崩溃比率  。
2. Microsoft 照片应用的崩溃总次数 = 计数（Microsoft 照片在具有该驱动程序的计算机上的崩溃次数） 
3. Microsoft 照片的总运行时 = 总和（具有该驱动程序的每台计算机的 Microsoft 照片运行时） 
4. 运行时（年）= Microsoft 照片的总运行时 \*60（分钟）\*60（小时）\*24（天）\*365（年） 

### <a name="final-calculation"></a>最终计算

按使用时间（年）规范化的 Microsoft 照片的崩溃次数 = Microsoft 照片的崩溃总次数/运行时（年） 
