---
title: 由于存在 Bitlocker 风险而挂起固件更新的计算机的百分比
description: 该度量将 28 天滑动窗口中的遥测数据聚合为被 Bitlocker 阻止的计算机数与尝试安装固件的计算机数的比率
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 97713be7e364044227397e0f5cdc516243abce10
ms.sourcegitcommit: c214e65a7f5dd868037718a34ca7cc80584df5c6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89615461"
---
# <a name="percent-of-machines-with-pending-firmware-updates-due-to-bitlocker-risk"></a>由于存在 Bitlocker 风险而挂起固件更新的计算机的百分比

## <a name="description"></a>说明

由于存在安装后进入 Bitlocker 恢复模式的风险而挂起固件更新的计算机的百分比 这是由于客户运行的版本低于带 2018 年 6 月累积更新的 Windows 10。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |零售和预览体验成员|
|时间段 |28 天滑动窗口|
|度量标准 |计算机的聚合|
|最小实例数 |250|
|通过标准 |<= 10%|
|度量 ID |23153969 或 23260737|

## <a name="calculation"></a>计算

被 Bitlocker 阻止的计算机数/

已尝试安装固件的计算机数

