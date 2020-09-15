---
title: 从 ESRT 报告成功安装固件的计算机的百分比
description: 该度量将 28 天滑动窗口中的遥测数据聚合为尝试安装时成功的比率
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 71b0aa542ac79023bc6d1ae8f45b3790d5ce4c69
ms.sourcegitcommit: c214e65a7f5dd868037718a34ca7cc80584df5c6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89615487"
---
# <a name="percent-of-machines-reporting-successful-firmware-installation-from-esrt"></a>从 ESRT 报告成功安装固件的计算机的百分比

## <a name="description"></a>说明

该度量将 28 天滑动窗口中的遥测数据聚合为尝试安装时成功的比率。
如果发生以下事件，则会将安装定义为成功的安装：

1. 设备实例以 UEFI 开头的固件通过 drvinst 进行了安装
2. 计算机重启，固件得到应用
3. 启动时 UEFI.sys 报告安装成功。


如果计算机报告了暂时性错误（下面列出了 UEFI.SYS 中的暂时性错误），则不会将其包括在总体中。

|错误代码|值|
|----|----|
|3221225659| STATUS_NOT_SUPPORTED|
|3221226195| STATUS_POWER_STATE_INVALID|
|3221226206| STATUS_INSUFFICIENT_POWER|
|3221225506| STATUS_ACCESS_DENIED|
|3221225473| STATUS_UNSUCCESSFUL|
|3221225517| STATUS_NOT_COMMITTED|
|3221225560| STATUS_UNKNOWN_REVISION|
|3221225626| STATUS_INSUFFICIENT_RESOURCES|
|3221226194| STATUS_PNP_REBOOT_REQUIRED|
|3221225659| STATUS_NOT_SUPPORTED|
|3221226195| STATUS_POWER_STATE_INVALID|
|3221226206| STATUS_INSUFFICIENT_POWER|
|3221225862| STATUS_DEVICE_PROTOCOL_ERROR|
|3221226681| STATUS_UNSATISFIED_DEPENDENCIES|
|3221226029| STATUS_RETRY|

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |零售和预览体验成员|
|时间段 |28 天滑动窗口|
|度量标准 |计算机的聚合|
|最小实例数 |200|
|通过标准 |>= 95%|
|度量 ID |20116729 或 23260700|

## <a name="calculation"></a>计算

成功的计算机数/尝试了固件设备且未处于暂时性状态的计算机数

