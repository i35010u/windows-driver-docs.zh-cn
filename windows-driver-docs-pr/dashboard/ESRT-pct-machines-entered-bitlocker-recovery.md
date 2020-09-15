---
title: 已更新且已成功解锁 Bitlocker 恢复的计算机的百分比
description: 该度量将 28 天滑动窗口中的遥测数据聚合为报告了 Bitlocker 恢复事件的计算机数与尝试安装固件的计算机数的比率
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: fc9f96dc06ddae65439f4686c3d4b9f7557e9728
ms.sourcegitcommit: c214e65a7f5dd868037718a34ca7cc80584df5c6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89615491"
---
# <a name="percent-of-machines-updated-and-successfully-unlocked-bitlocker-recovery"></a>已更新且已成功解锁 Bitlocker 恢复的计算机的百分比

## <a name="description"></a>说明

已安装固件并进入 Bitlocker 恢复模式（因此客户可以通过输入 Bitlocker 恢复密钥进行恢复）的计算机的百分比

该度量将 28 天滑动窗口中的遥测数据聚合为报告了 Bitlocker 恢复事件的计算机数与尝试安装固件的计算机数的比率

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |零售和预览体验成员|
|时间段 |28 天滑动窗口|
|度量标准 |计算机的聚合|
|最小实例数 |250|
|通过标准 |<= 10%|
|度量 ID |23154031 或 23260740|

## <a name="calculation"></a>计算

在启动时报告了 Bitlocker 恢复事件的计算机数/

已尝试安装固件的计算机数

