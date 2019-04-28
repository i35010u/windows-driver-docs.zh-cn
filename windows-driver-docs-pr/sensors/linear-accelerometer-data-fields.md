---
title: 线性加速计数据字段
description: 本主题提供有关特定于线性加速感应器数据字段的信息。
ms.assetid: FD869359-C1C2-4B2F-95F3-01234331DC54
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: af80e0005d950244506d928cc8bb2a325b73a013
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345155"
---
#  <a name="linear-accelerometer-data-fields"></a>线性加速计数据字段

本主题提供有关特定于线性加速感应器数据字段的信息。

下表显示数据字段。 有关类型列中显示的类型的详细信息，请参阅[MSDN PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|在任务栏的搜索框中键入|必需/可选|描述|
|--|--|--|--|
|PKEY_SensorData_AccelerationX_Gs|VT_R4|必需|G's 中 x 轴加速|
|PKEY_SensorData_AccelerationY_Gs|VT_R4|必需|在 g's y 轴加速|
|PKEY_SensorData_AccelerationZ_Gs|VT_R4|必需|在 g's z 轴加速|
|PKEY_SensorData_Shake|VT_BOOL|可选|指示一摇还被线性加速感应器检测到。 这必须是如果数据字段被发送，则为 true。|

 

## <a name="related-topics"></a>相关主题


[MSDN PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)





