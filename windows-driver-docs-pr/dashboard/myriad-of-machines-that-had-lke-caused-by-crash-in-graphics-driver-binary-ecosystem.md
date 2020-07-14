---
title: 由于显卡驱动程序二进制文件中的崩溃导致发生了 LKE 的计算机的巨大数量
description: 该度量将来自 7 天滑动窗口的遥测数据聚合为大量不同计算机，这些计算机由于显卡驱动程序二进制文件中的崩溃而发生了 LKE
ms.topic: article
ms.date: 10/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: 79e151e3087d62a09fb122d062f0045819b171a5
ms.sourcegitcommit: cb5f370b867ceab28b6b6c64a3586b0bb3831b3d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86035993"
---
# <a name="myriad-of-machines-that-had-an-lke-caused-by-a-crash-in-the-graphics-driver-binary-ecosystem"></a>由于显卡驱动程序二进制文件中的崩溃导致发生了 LKE 的计算机的巨大数量（生态系统）

## <a name="description"></a>描述

在用户会话期间，显卡驱动程序二进制文件中的崩溃可能导致实时内核事件 (LKE)，该事件可能会重启计算机，并且可能会中断用户的工作流。 该度量评估由于显卡驱动程序二进制文件中的崩溃而导致遇到 LKE 的使用该驱动程序的计算机数。

这是[由于显卡驱动程序二进制文件中的崩溃导致出现 LKE 的计算机的巨大数量](https://docs.microsoft.com/windows-hardware/drivers/dashboard/myriad-of-machines-that-had-lke-caused-by-crash-in-graphics-driver-binary-standard)度量的生态系统对应项。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众|生态系统|
|时间段|7 天滑动窗口|
|度量标准|计算机的聚合|
|最小总体数量|20,000 台计算机|
|通过标准|<= 130/10,000 台计算机遇到 LKE 事件|
|度量 ID|17361846|

## <a name="calculation"></a>计算

该度量将来自 7 天滑动窗口的遥测数据聚合为**大量**的**不同计算机，这些计算机由于显卡驱动程序二进制文件中的崩溃而发生了 LKE**。
1. 出现 LKE 的计算机数 = 计数（使用该驱动程序的计算机中出现 LKE 的计算机数）
2. 计算机总数 = 计数（使用该驱动程序的计算机数）
3. 发生 LKE 的计算机的比率 = 发生 LKE 的计算机数/计算机总数

### <a name="final-calculation"></a>最终计算

相对于总体的不同设备命中数 (DHoP) = 出现 LKE 的计算机的比率 * 10,000

在上面的计算中，结果规范化为 10,000 台计算机，最终结果为：    
[相对于总体的不同设备命中数 (DHoP)] 10,000 台计算机中由于显卡驱动程序二进制文件中的崩溃而发生 LKE 的不同计算机数
