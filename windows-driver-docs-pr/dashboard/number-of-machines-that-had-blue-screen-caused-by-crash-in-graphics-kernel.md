---
title: 显卡内核中的崩溃导致出现蓝屏的计算机数
description: 该度量将来自 7 天滑动窗口的遥测数据聚合为大量不同计算机，这些计算机由于显卡内核中的崩溃发生蓝屏
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: e421c489a67692d8afcde9b51dc4ccf6804a448c
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "71016979"
---
# <a name="number-of-machines-that-had-a-blue-screen-caused-by-a-crash-in-the-graphics-kernel"></a>显卡内核中的崩溃导致出现蓝屏的计算机数

## <a name="description"></a>说明

在用户会话期间，显卡内核中的崩溃将导致蓝屏，这会重启计算机，并且可能会中断用户的工作流。 该度量评估使用该驱动程序的计算机中遇到显卡内核崩溃的计算机数。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |Standard|
|时间段 |7 天滑动窗口|
|度量标准 |计算机的聚合|
|最小总体数量 |5,000 台计算机|
|通过标准 |<= 10/10,000 台计算机的显示内核中出现崩溃|
|度量 ID |7533022|

## <a name="calculation"></a>计算

1. 该度量将来自 7 天滑动窗口的遥测数据聚合为大量不同计算机，这些计算机由于显卡内核中的崩溃发生蓝屏（相对于总体）   。
2. 出现蓝屏的计算机数 = 计数（使用该驱动程序的计算机中出现蓝屏的计算机数） 
3. 计算机总数 = 计数（使用该驱动程序的计算机数） 
4. 蓝屏计算机的比率 = 出现蓝屏的计算机数/计算机总数 

### <a name="final-calculation"></a>最终计算

5. 相对于总体的蓝屏计算机命中数 = 蓝屏计算机的比率 * 10,000 
6. 结果规范化为 10,000 台计算机，最终计算为：

   i. [相对于总体的蓝屏计算机命中数] 10,000 台计算机中由于显卡驱动程序二进制文件中的崩溃而发生蓝屏的不同计算机数