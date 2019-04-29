---
title: 传感器结构
description: 传感器结构
ms.assetid: 94194998-8A56-48D3-9053-007526BF0ED2
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 62e6bbf7173d4e813fa73cc0c1ca34246befaac9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368807"
---
# <a name="sensor-structures"></a>传感器结构

本部分包含有关传感器结构，并提供对各种属性和传感器功能的访问信息。

## <a name="in-this-section"></a>本节内容

|主题|描述|
|---|---|
|[SENSOR_VALUE_PAIR](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_value_pair)|此结构对每个键表示的数据的传感器属性部分中列出的属性键。|
|[SENSOR_COLLECTION_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)|此结构包含每个传感器的所有 SENSOR_VALUE_PAIR 结构的列表。|
|[SENSOR_PROPERTY_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_property_list)|此结构包含每个传感器的所有 SENSOR_VALUE_PAIR 结构的列表。|
|[SENSOR_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_config)|此结构包含传感器驱动程序将传递到关于每个传感器类扩展的信息。|
|[SENSOR_CONTROLLER_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)|此结构包含必须由该驱动程序，并传递到要调用的类扩展的回调函数的指针。|
|SENSOR_DATA|此结构定义其他传感器可用于定义特定于传感器的数据类型的基类型。|
|SENSOR_DEVICE_CAPS|此结构描述传感器组件的功能。|
|SENSOR_DATA_HEADER|此结构包含有关传感器读数的信息。|
|VEC3D|此结构保存三维定位数据的单个数据点。|
|四元数|此结构用于表示用于简单的三维旋转操作 4 维矢量。|
|MATRIX3X3|此结构用于表示泛型 3x3 矩阵。|






