---
title: 线性加速计数据字段
description: 本主题提供有关特定于线性加速度的数据字段的信息。
ms.assetid: FD869359-C1C2-4B2F-95F3-01234331DC54
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 067a93564a17349f9e7c3682f8def86fdc9f5d05
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732785"
---
#  <a name="linear-accelerometer-data-fields"></a>线性加速计数据字段

本主题提供有关特定于线性加速度的数据字段的信息。

下表显示了数据字段。 有关 "类型" 列中显示的类型的详细信息，请参阅 [MSDN PROPVARIANT structure](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)。

|属性键|类型|必需/可选|说明|
|--|--|--|--|
|PKEY_SensorData_AccelerationX_Gs|VT_R4|必须|G 中的 x 轴加速度。|
|PKEY_SensorData_AccelerationY_Gs|VT_R4|必须|G 中的 y 轴加速度。|
|PKEY_SensorData_AccelerationZ_Gs|VT_R4|必须|G 的 z 轴加速度。|
|PKEY_SensorData_Shake|VT_BOOL|可选|指示已由线性加速度检测到晃动。 如果发送数据字段，则必须为 true。|

 

## <a name="related-topics"></a>相关主题


[MSDN PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)