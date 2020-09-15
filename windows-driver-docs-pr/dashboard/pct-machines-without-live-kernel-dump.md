---
title: 具有实时内核转储的计算机所占的百分比
description: 该度量将 7 天滑动窗口中的遥测数据进行聚合并形成经历了实时内核转储的计算机所占的百分比
ms.topic: article
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1c7f8803df1d4db454b8b8e0644da3af1dd38c5f
ms.sourcegitcommit: c214e65a7f5dd868037718a34ca7cc80584df5c6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89615469"
---
# <a name="percent-of-machines-without-a-live-kernel-dump"></a>没有实时内核转储的计算机所占的百分比

## <a name="description"></a>说明

实时内核转储 (LKD) 是内核错误的结果，遇到这种情况时，计算机可以恢复而不发生崩溃。 如果用户遇到 LKD，其应用程序可能会挂起或崩溃。 一种常见类型的 LKD 是超时检测和恢复 (TDR)，在此情况下，在驱动程序恢复之前，显卡驱动程序会崩溃，并且显示器会暂时变黑。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众|Standard|
|时间段|7 天滑动窗口|
|度量标准|计算机的聚合|
|最小总体数量|100 台计算机|
|通过标准|<= 3% 的计算机遇到了 LKD|
|已启用队列|是|
|每队列最小总体数量|500 台计算机|
|度量 ID|25739929 或 26118015|

## <a name="calculation"></a>计算

1. 该度量将 7 天滑动窗口中的遥测数据进行聚合并形成经历了 LKD 的计算机所占的百分比
2. 经历了 LKD 的计算机数 = 计数（安装驱动程序时遇到 LKD 的计算机数）
3. 计算机总数 = 计数（已成功安装驱动程序的计算机数）

### <a name="final-calculation"></a>最终计算

未经历 LKD 的计算机的百分比 = 经历了 LKD 的计算机数/计算机总数
