---
title: 由于存在 Bitlocker 风险而挂起固件更新的计算机的百分比
description: 该度量将 28 天滑动窗口中的遥测数据聚合为被 Bitlocker 阻止的计算机数与尝试安装固件的计算机数的比率
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5591405275835f2a00aa9e2d11c56444bdf3e1cc
ms.sourcegitcommit: 07b2926c15f4782e1914e8d3cf6c5c511a3a6111
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/14/2019
ms.locfileid: "74097503"
---
# <a name="percent-of-machines-with-pending-firmware-updates-due-to-bitlocker-risk"></a>由于存在 Bitlocker 风险而挂起固件更新的计算机的百分比

## <a name="description"></a>描述

由于存在安装后进入 Bitlocker 恢复模式的风险而挂起固件更新的计算机的百分比 这是由于客户运行的版本低于带 2018 年 6 月累积更新的 Windows 10。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |零售和预览体验成员|
|时间段 |28 天滑动窗口|
|度量标准 |计算机的聚合|
|最小实例数 |250|
|通过标准 |>= 90%|
|度量 ID |23153969|

## <a name="calculation"></a>计算

被 Bitlocker 阻止的计算机数/

已尝试安装固件的计算机数

