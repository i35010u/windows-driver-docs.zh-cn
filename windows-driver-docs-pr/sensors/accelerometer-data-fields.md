---
title: 加速计数据字段
description: 本主题提供有关特定于加速度的数据字段的信息。
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 833115b8da6d14deaa277858fbe9fe1a0a0db58e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812395"
---
# <a name="accelerometer-data-fields"></a>加速计数据字段


本主题提供有关特定于加速度的数据字段的信息。

下表显示了数据字段。 有关 "类型" 列中显示的类型的详细信息，请参阅 [PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)。

|属性键|类型|必需/可选|说明|
| --- | --- | --- | --- |
|PKEY_SensorData_AccelerationX_Gs|VT_R4|必须|G 中的 x 轴加速度。|
|PKEY_SensorData_AccelerationY_Gs|VT_R4|必须|G 中的 y 轴加速度。|
|PKEY_SensorData_AccelerationZ_G|VT_R4|必须|G 的 z 轴加速度。|
|PKEY_SensorData_Shake|VT_BOOL|可选|指示已由加速度检测到晃动。 如果发送数据字段，则必须为 true。|

 

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)

 

