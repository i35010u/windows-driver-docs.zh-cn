---
title: 相对方向传感器数据字段
description: 本主题提供有关特定于相对方向传感器的数据字段的信息。
ms.assetid: A48B75DD-5424-48CC-AC8B-251874414FCE
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: d4929435b09512c445140d60ea496dc811f1ab57
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733135"
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

 

