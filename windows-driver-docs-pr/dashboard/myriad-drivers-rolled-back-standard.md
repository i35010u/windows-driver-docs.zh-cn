---
title: 在安装后的 2 天内回滚或重新安装的驱动程序的巨大数量
description: 该度量将来自 7 天滑动窗口的遥测数据聚合为大量不同的计算机，这些计算机在安装后 2 天内回滚或重新安装
ms.topic: article
ms.date: 05/11/2020
ms.localizationpriority: medium
ms.openlocfilehash: a7823743882ee93278a09a7606af5c17da60de03
ms.sourcegitcommit: d7b5e6049db3109fdcbe83279875f24f3fa6acdd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "84110237"
---
# <a name="myriad-of-drivers-that-were-rolled-back-or-re-installed-within-2-days-of-installation"></a>在安装后的 2 天内回滚或重新安装的驱动程序的巨大数量

## <a name="description"></a>说明

该度量跟踪驱动程序在安装后 2 天内是回滚还是通过安装另一驱动程序才能成功（不由 WU 启动）。 此类操作表示用户遇到足够严重的驱动程序以致于需要使用另一个驱动程序。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众|驱动程序的目标设备|
|时间段|7 天滑动窗口|
|度量标准|计算机计数|
|最小总体数量|5,000 台设备|
|通过标准|安装驱动程序的每 10,000 台设备的回滚次数小于等于 10|
|度量 ID|19564492|

## <a name="calculation"></a>计算

该度量将来自 7 天滑动窗口的遥测数据聚合为安装驱动程序的每 10,000 台设备中驱动程序回滚次数与安装另一驱动程序的次数之比

回滚或安装另一驱动程序的设备总数 = 计数（在驱动程序安装后 2 天内回滚或安装另一驱动程序的设备数）

设备总数 = 计数（安装驱动程序并将它使用 2 天的设备数）

### <a name="final-calculation"></a>最终计算

驱动程序回滚次数与安装另一驱动程序次数之比 = 已回滚或已安装另一驱动程序的设备总数 * 10,000/设备总数
