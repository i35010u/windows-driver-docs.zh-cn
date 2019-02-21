---
title: 加速感应器数据字段
description: 本主题提供有关特定于加速感应器数据字段的信息。
ms.assetid: 88333B6A-E262-4937-9349-156B00BA8CC4
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: f2d8883d56e3180559e52271b75b787bfda33360
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543576"
---
# <a name="accelerometer-data-fields"></a>加速感应器数据字段


本主题提供有关特定于加速感应器数据字段的信息。

下表显示数据字段。 有关类型列中显示的类型的详细信息，请参阅[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|在任务栏的搜索框中键入|必需/可选|描述|
| --- | --- | --- | --- |
|PKEY_SensorData_AccelerationX_Gs|VT_R4|必需|G's 中 x 轴加速|
|PKEY_SensorData_AccelerationY_Gs|VT_R4|必需|在 g's y 轴加速|
|PKEY_SensorData_AccelerationZ_G|VT_R4|必需|在 g's z 轴加速|
|PKEY_SensorData_Shake|VT_BOOL|可选|指示一摇还被加速感应器检测到。 这必须是如果数据字段被发送，则为 true。|

 

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






