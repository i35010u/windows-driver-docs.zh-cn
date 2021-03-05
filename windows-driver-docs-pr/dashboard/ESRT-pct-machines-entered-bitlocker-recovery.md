---
title: 已更新且已成功解锁 Bitlocker 恢复的计算机的百分比
description: 该度量将 28 天滑动窗口中的遥测数据聚合为报告了 Bitlocker 恢复事件的计算机数与尝试安装固件的计算机数的比率
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6602411cc4091befbd15e1aa5c20ac00ee9276d3
ms.sourcegitcommit: ac28dd2a921c25796d19572a180b88e460420488
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2021
ms.locfileid: "101682272"
---
# <a name="percent-of-machines-updated-and-successfully-unlocked-bitlocker-recovery"></a>已更新且已成功解锁 Bitlocker 恢复的计算机的百分比

## <a name="description"></a>说明

已安装固件并进入 Bitlocker 恢复模式（因此客户可以通过输入 Bitlocker 恢复密钥进行恢复）的计算机的百分比

该度量将 28 天滑动窗口中的遥测数据聚合为报告了 Bitlocker 恢复事件的计算机数与尝试安装固件的计算机数的比率

在安装新固件后请求 Bitlocker 恢复密钥最常见的原因是平台配置注册 (PCR) 7 具有不可接受的 Bitlocker 封装度量值，因此 Bitlocker 读取旧版 PCR，包括 PCR 0。 由于 PCR 0 将在固件更新时发生更改，因此 Bitlocker 将触发恢复。 要进行调试，请查看其中一个设备，了解 PCR 7 中的功能，然后检查固件包的组件是否添加了任何会导致出现此情况的机制（调试、dma 保护关闭、可选 rom、第三方预启动 fw 等）。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |零售和预览体验成员|
|时间段 |28 天滑动窗口|
|度量标准 |计算机的聚合|
|最小实例数 |170|
|通过标准 |<= 5%|
|度量 ID |23260740|

## <a name="calculation"></a>计算

在启动时报告了 Bitlocker 恢复事件的计算机数/

已尝试安装固件的计算机数

