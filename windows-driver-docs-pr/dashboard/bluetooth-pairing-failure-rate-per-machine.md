---
title: 蓝牙配对失败次数百分比
description: ''
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 85ec8300e547130bdd9b665175e41a1a12022ac8
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2019
ms.locfileid: "71017085"
---
# <a name="percent-of-bluetooth-pairing-failures"></a>蓝牙配对失败次数百分比

## <a name="description"></a>描述

成功完成蓝牙配对后，身份验证信息会在本地保存，供将来使用。 如果设备无法配对，则用户将无法对其连接进行身份验证，并且无法在设备之间流式传输内容。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |Standard|
|时间段 |7 天滑动窗口|
|度量标准 |实例的聚合|
|最小总体数量 |10 个实例|
|通过标准 |<= 5% 的实例出现配对失败|
|度量 ID |14612509|

## <a name="calculation"></a>计算

1. 该度量将 7 天滑动窗口中的遥测数据聚合为蓝牙设备无法与其他设备配对的实例所占的百分比  。

   a. 单个计算机中可以有多种通过度量进行计数的配对实例 

2. 实例类型：

   a. 成功配对事件 = 0% 失败 

   b. 配对取消事件或中性配对 = 5% 失败 

   c. 超时 = 20% 失败 

   d. 配对失败事件 = 100% 失败 

### <a name="final-calculation"></a>最终计算

蓝牙配对失败率 = 平均值（所有实例） 