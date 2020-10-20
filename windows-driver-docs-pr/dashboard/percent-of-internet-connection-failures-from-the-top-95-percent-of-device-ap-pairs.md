---
title: 信号质量大于 50% 的设备和接入点对的 Internet 连接失败次数百分比
description: 该度量将来自 7 天滑动窗口的遥测数据聚合为设备无法通过 Wi-Fi 连接到 Internet 的实例所占的百分比。
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5a0c3773175852458ed15cdaf5b2b271317ae5ad
ms.sourcegitcommit: 068a9875851a278935078ba7f1ab65a3bb37235c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2020
ms.locfileid: "92100392"
---
# <a name="percent-of-internet-connection-failures-of-device-and-access-point-pairs-that-have-greater-than-50-percent-signal-quality"></a>信号质量大于 50% 的设备和接入点对的 Internet 连接失败次数百分比

## <a name="description"></a>说明

设备连接到接入点 (AP) 后，可使用该连接尝试通过 Wi-Fi 连接到 Internet。 如果用户无法使用 Wi-Fi 连接到 Internet，则会在“Internet 访问”按钮上显示警告图标（黄色区域内显示惊叹号）。 用户无法完全运行需要 Wi-Fi 的应用程序。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |Standard|
|时间段 |7 天|
|度量标准 |实例的聚合|
|最小实例数 |3,000|
|通过标准 |<= 10% 的实例无法通过 Wi-Fi 连接到 Internet|
|度量 ID |25975470|

## <a name="calculation"></a>计算

1. 该度量将来自 7 天滑动窗口的遥测数据聚合为设备无法通过 Wi-Fi 连接到 Internet 的实例所占的百分比  。

   a. 实例是计算机与唯一 AP 之间的配对；根据“设备–AP”对，该度量聚合通过 Wi-Fi 连接到 Internet（以连接单一数据点）的每次尝试连接。

   b. 如果信号强度低于 50%，则该度量不会聚合任何“设备–AP”对。

2. 连接失败计为“100”，连接成功计为“0”

### <a name="final-calculation"></a>最终计算

“设备–AP”对到 Internet 的连接失败率 = 平均值（所有实例） 