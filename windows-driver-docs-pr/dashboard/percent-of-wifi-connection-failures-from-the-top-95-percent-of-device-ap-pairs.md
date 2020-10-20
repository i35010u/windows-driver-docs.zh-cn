---
title: 信号质量大于 50% 的设备和接入点对的 Wi-Fi 连接失败次数百分比
description: 该度量将来自 7 天滑动窗口的遥测数据聚合为设备无法连接到接入点的实例所占的百分比
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: d0dd467df423b7711ed59ad4969ca5ea7e7fd9c9
ms.sourcegitcommit: 068a9875851a278935078ba7f1ab65a3bb37235c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2020
ms.locfileid: "92100398"
---
# <a name="percent-of-wi-fi-connection-failures-from-devices-and-access-point-pairs-that-have-greater-than-50-percent-signal-quality"></a>信号质量大于 50% 的设备和接入点对的 Wi-Fi 连接失败次数百分比 

## <a name="description"></a>说明

Wi-Fi 接入点 (AP) 是一种网络硬件，可允许其他启用 Wi-Fi 的设备连接到无线局域网 (WLAN)。 用户无法连接到 AP 时，其计算机显示“无法连接到接入点”错误消息，并将无法访问 WLAN 或 Wi-Fi  。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |目标 HWID 和 CHID|
|时间段 |7 天|
|度量标准 |实例的聚合 |
|最小实例数 |3,000|
|通过标准 |<= 6% 的实例发生 AP 连接失败 |
|度量 ID |25975432|

## <a name="calculation"></a>计算

1. 该度量将来自 7 天滑动窗口的遥测数据聚合为设备无法连接到 AP 的实例所占的百分比 

   a. 实例是设备与唯一 AP 之间的配对；根据设备，该度量聚合到唯一 AP 的每次尝试连接。

   b. 如果信号强度低于 50%，则该度量不会聚合任何“设备–AP”对。

2. 连接失败计为“100”，连接成功计为“0”

### <a name="final-calculation"></a>最终计算

“设备–AP”对的连接失败率 = 平均值（所有实例） 