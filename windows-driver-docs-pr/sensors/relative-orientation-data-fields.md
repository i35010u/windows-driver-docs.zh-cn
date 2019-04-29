---
title: 相对方向传感器数据字段
description: 本主题提供有关特定于相对方向传感器的数据字段的信息。
ms.assetid: A48B75DD-5424-48CC-AC8B-251874414FCE
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 435b906ec74bd1c76d6365324f5de40af44d6a16
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358541"
---
# <a name="relative-orientation-sensor-data-fields"></a>相对方向传感器数据字段


本主题提供有关特定于相对方向传感器的数据字段的信息。

下表显示数据字段。 有关类型列中显示的类型的详细信息，请参阅[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|在任务栏的搜索框中键入|必需/可选|描述|
|--|--|--|--|
|PKEY_SensorData_Timestamp|VT_FILETIME|必需|采样的数据的时间戳。 这是必需的传感器驱动程序报告每个示例。|
|PKEY_SensorData_QuaternionW|VT_R4|必需|（而不是复数的虚部部分） 的真实系数。|
|PKEY_SensorData_QuaternionX|VT_R4|必需|旋转轴向量的 X 分量。|
|PKEY_SensorData_QuaternionY|VT_R4|必需|旋转轴向量的 X 分量。|
|PKEY_SensorData_QuaternionZ|VT_R4|必需|旋转轴向量的 X 分量。|

 

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






