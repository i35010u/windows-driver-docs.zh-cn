---
title: 没有内核模式崩溃的计算机所占的百分比
description: 该度量将 14 天滑动窗口中的遥测数据聚合为未经历内核模式崩溃的计算机所占的百分比
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 49540d0393a8423721ce9255c636c0f6c0ce29fa
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "71016946"
---
# <a name="percent-of-machines-without-a-kernel-mode-crash"></a>没有内核模式崩溃的计算机所占的百分比

## <a name="description"></a>说明

内核模式崩溃 (KMC) 由停止操作系统的内核错误导致。 如果用户遇到 KMC，其计算机会突然崩溃，并显示蓝屏。 此类崩溃可能会导致用户工作流中断，并且导致数据丢失。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |Standard|
|时间段 |14 天滑动窗口|
|度量标准 |计算机的聚合|
|最小总体数量 |100 台计算机|
|通过标准 |>= 96% 的计算机未遇到内核模式崩溃|
|度量 ID |19888712|

## <a name="calculation"></a>计算

1. 该度量将 14 天滑动窗口中的遥测数据聚合为未经历 KMC 的计算机所占的百分比 
2. 未崩溃的计算机数 = 计数（安装了驱动程序且没有 KMC 的计算机） 
3. 计算机总数 = 计数（已成功安装驱动程序的计算机数） 

### <a name="final-calculation"></a>最终计算

没有 KMC 的计算机的百分比 = 未崩溃的计算机数/计算机总数 
