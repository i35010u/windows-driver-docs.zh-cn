---
title: 从低功率状态恢复时出现显示问题的计算机的百分比
description: 该度量将来自 7 天滑动窗口的遥测数据聚合为从低功率状态恢复时出现显示问题的计算机的百分比
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: faa827ff80942ed5acfbde3c84e7eda5f77bf1fb
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2019
ms.locfileid: "71017069"
---
# <a name="percent-of-machines-with-display-issues-when-resume-from-low-power-state"></a>从低功率状态恢复时出现显示问题的计算机的百分比

## <a name="description"></a>描述

计算机从低功率状态启动时，显卡组件中的错误会导致出现影响用户体验的显示问题。 此度量计算在低功率状态下恢复时出现显示问题的计算机的百分比。 有关显示问题的列表，请参阅[附录](measure-appendix.md#display-issues)。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |生态系统|
|时间段 |7 天滑动窗口|
|度量标准 |计算机的聚合|
|最小总体数量 |100 台处于低功率状态的计算机|
|通过标准 |<= 0.8% 处于低功率状态的计算机遇到显示问题|
|度量 ID |19920755|

## <a name="calculation"></a>计算

1. 该度量将来自 7 天滑动窗口的遥测数据聚合为从低功率状态恢复时出现显示问题的计算机的百分比  。
2. 出现显示问题的计算机数 = 计数（从低功率状态恢复时出现问题的计算机数） 
3. 计算机总数 = 计数（在外部测试过程中执行低到高功率状态转换的计算机数） 

### <a name="final-calculation"></a>最终计算

从低功率状态恢复时出现显示问题的计算机的百分比 = 出现显示问题的计算机数/计算机总数 
