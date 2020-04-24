---
title: WLAN 连接失败次数百分比（来自前 95% 的设备和接入点对）
description: 该度量将来自 7 天滑动窗口的遥测数据聚合为设备无法连接到接入点的实例所占的百分比
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: e8ac44992816693a18b1e8ae3d265949d74b2d5f
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "71016949"
---
# <a name="percent-of-wi-fi-connection-failures-from-the-top-95-percent-of-device-and-access-point-pairs"></a>WLAN 连接失败次数百分比（来自前 95% 的设备和接入点对） 

## <a name="description"></a>说明

Wi-Fi 接入点 (AP) 是一种网络硬件，可允许其他启用 Wi-Fi 的设备连接到无线局域网 (WLAN)。 用户无法连接到 AP 时，其计算机显示“无法连接到接入点”错误消息，并将无法访问 WLAN 或 Wi-Fi  。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |目标 HWID 和 CHID|
|时间段 |7 天|
|度量标准 |实例的聚合 |
|最小实例数 |3,000|
|通过标准 |<= 2% 的实例发生 AP 连接失败 |
|度量 ID |14642524|

## <a name="calculation"></a>计算

1. 该度量将来自 7 天滑动窗口的遥测数据聚合为设备无法连接到 AP 的实例所占的百分比 

   a. 实例是设备与唯一 AP 之间的配对；根据设备，该度量聚合到唯一 AP 的每次尝试连接。

   b. 如果信号强度低于 50%，则该度量不会聚合任何“设备–AP”对。

   c. 如果“设备–AP”对的连接率在“设备–AP”对中排在最后 5%，则该度量不会聚合此对。

2. 连接失败计为“100”，连接成功计为“0”

### <a name="final-calculation"></a>最终计算

“设备–AP”对的连接失败率 = 平均值（所有实例） 