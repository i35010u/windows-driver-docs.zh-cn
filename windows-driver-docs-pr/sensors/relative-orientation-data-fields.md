---
title: 相对方向传感器数据字段
description: 本主题提供有关特定于相对方向传感器的数据字段的信息。
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: e57e20fe5c898afac5b0d37f4eab750c8d418611
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812249"
---
# <a name="relative-orientation-sensor-data-fields"></a>相对方向传感器数据字段


本主题提供有关特定于相对方向传感器的数据字段的信息。

下表显示了数据字段。 有关 "类型" 列中显示的类型的详细信息，请参阅 [PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)。

|属性键|类型|必需/可选|说明|
|--|--|--|--|
|PKEY_SensorData_Timestamp|VT_FILETIME|必须|采样数据的时间戳。 这对于传感器驱动程序报告的每个示例都是必需的。|
|PKEY_SensorData_QuaternionW|VT_R4|必须|实系数 (相对于复数的虚部) 。|
|PKEY_SensorData_QuaternionX|VT_R4|必须|旋转轴向量的 X 分量。|
|PKEY_SensorData_QuaternionY|VT_R4|必须|旋转轴向量的 X 分量。|
|PKEY_SensorData_QuaternionZ|VT_R4|必须|旋转轴向量的 X 分量。|

 

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)

 

