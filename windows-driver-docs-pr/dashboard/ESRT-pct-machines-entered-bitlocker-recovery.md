---
title: 已更新且已成功解锁 Bitlocker 恢复的计算机的百分比
description: 该度量将 28 天滑动窗口中的遥测数据聚合为报告了 Bitlocker 恢复事件的计算机数与尝试安装固件的计算机数的比率
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 091c4d62efa703ddd0f600617ad8da72ed9e13ea
ms.sourcegitcommit: 5e51e63585f35597cf06fc0ab5c0cc7cb39ca22a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "98861855"
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
|最小实例数 |170|
|通过标准 |<= 5%|
|度量 ID |23260740|

## <a name="calculation"></a>计算

在启动时报告了 Bitlocker 恢复事件的计算机数/

已尝试安装固件的计算机数

