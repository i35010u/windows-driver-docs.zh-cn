---
title: 蓝牙连接失败次数百分比
description: 该度量将 7 天滑动窗口中的遥测数据聚合为蓝牙设备未能连接其他设备的实例所占的比例。
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: f7df03da49a8be8b7119aafe4ff6da97b1e90349
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2019
ms.locfileid: "71017089"
---
# <a name="percent-of-bluetooth-connection-failures"></a>蓝牙连接失败次数百分比

## <a name="description"></a>描述

如果两个设备无法与蓝牙连接，则用户将无法向另一个设备发送内容或者接收来自另一个设备的内容。 断开连接也可能表明设备之间存在通信问题。 该度量计算蓝牙连接的失败率。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |Standard|
|时间段 |7 天滑动窗口|
|度量标准 |实例的聚合|
|最小总体数量 |10 个实例|
|通过标准 |< 10 % 的实例为连接失败|
|度量 ID |13897278|

## <a name="calculation"></a>计算

1. 该度量将 7 天滑动窗口中的遥测数据聚合为蓝牙设备未能连接其他设备的实例所占的比例  。

   a. 单个设备中可以有多钟通过度量进行计数的配对实例

2. 实例类型：

   a. 成功的连接或断开连接事件 = 0% 失败 

   b. 连接失败或成功断开连接 = 100% 失败 

### <a name="final-calculation"></a>最终计算

蓝牙连接失败率 = 平均值（所有实例） 