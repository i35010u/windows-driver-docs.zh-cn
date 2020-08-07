---
title: 相机初始化失败次数百分比
description: 该度量将 7 天滑动窗口中的遥测数据聚合为相机设备未能初始化的实例所占的百分比
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 24c5e22e06aa906562bfe8b818e7ba7b3214db67
ms.sourcegitcommit: 20a89aa2cb2c6385c2a49ebf78e5797c821d87ab
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2020
ms.locfileid: "87473745"
---
# <a name="percent-of-camera-initialization-failures"></a>相机初始化失败次数百分比

## <a name="description"></a>说明

当某个用户尝试使用可访问计算机的相机设备的应用程序时，必须首先初始化相机功能。 如果此初始化失败，则用户无法使用计算机的相机来捕获内容，并且必须重启初始化过程。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众|Standard|
|时间段|7 天滑动窗口|
|度量标准|实例的聚合|
|最小总体数量|10 个实例|
|通过标准|<= 5% 的实例导致初始化失败|
|度量 ID|16998810|

## <a name="calculation"></a>计算

1. 该度量将 7 天滑动窗口中的遥测数据聚合为相机设备未能初始化的实例所占的百分比  。

   a. 唯一设备可以每小时计一个初始化实例。

2. 实例类型：

   a. 成功的初始化事件 = 0% 失败

```cpp
MF_CAPTURE_ENGINE_INITIALIZED with an HRESULT == 0
```

   b. 失败的初始化事件 = 100% 失败 

```cpp
i. MF_E_NO_CAPTURE_DEVICES_AVAILABLE

ii. E_ACCESSDENIED

iii. ERROR_BAD_UNIT
```

### <a name="final-calculation"></a>最终计算

相机初始化失败率 = 平均值（所有实例）