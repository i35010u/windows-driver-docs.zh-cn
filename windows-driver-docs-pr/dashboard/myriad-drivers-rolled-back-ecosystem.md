---
title: 在安装后的 2 天内回滚或重新安装的驱动程序的巨大数量（生态系统）
description: 该度量将来自 7 天滑动窗口的遥测数据聚合为大量不同的计算机，这些计算机在安装后 2 天内回滚或重新安装（生态系统）
ms.topic: article
ms.date: 05/11/2020
ms.localizationpriority: medium
ms.openlocfilehash: 19cc17511b1dc66f52593f1945c3ba03318fd463
ms.sourcegitcommit: 4f08f5686c0bbc27d58930b993cbab1a98e3afb0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89443799"
---
# <a name="myriad-of-drivers-that-were-rolled-back-or-re-installed-within-2-days-of-installation-ecosystem"></a>在安装后的 2 天内回滚或重新安装的驱动程序的巨大数量（生态系统）

## <a name="description"></a>描述

该度量跟踪驱动程序在安装后 2 天内是回滚还是通过安装另一驱动程序才能成功（不由 WU 启动）。 此类操作表示用户遇到足够严重的驱动程序以致于需要使用另一个驱动程序。

对于[在安装后的 2 天内回滚或重新安装的驱动程序的巨大数量](./myriad-drivers-rolled-back-standard.md)这一度量，这是它在生态系统中的对应项。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众|生态系统|
|时间段|7 天滑动窗口|
|度量标准|计算机计数|
|最小总体数量|5,000 台设备|
|通过标准|安装驱动程序的每 10,000 台设备的回滚次数小于等于 10|
|度量 ID|26124773|

## <a name="calculation"></a>计算

该度量将来自 7 天滑动窗口的遥测数据聚合为安装驱动程序的每 10,000 台设备中驱动程序回滚次数与安装另一驱动程序的次数之比

回滚或安装另一驱动程序的设备总数 = 计数（在驱动程序安装后 2 天内回滚或安装另一驱动程序的设备数）

设备总数 = 计数（安装驱动程序并将它使用 2 天的设备数）

### <a name="final-calculation"></a>最终计算

驱动程序回滚次数与安装另一驱动程序次数之比 = 已回滚或已安装另一驱动程序的设备总数 * 10,000/设备总数
