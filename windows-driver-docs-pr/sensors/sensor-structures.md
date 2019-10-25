---
title: 传感器结构
description: 传感器结构
ms.assetid: 94194998-8A56-48D3-9053-007526BF0ED2
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 78ff6b52c5dc652c99caa3b0a2b671c6614cae26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845490"
---
# <a name="sensor-structures"></a>传感器结构

本部分包含有关传感器结构的信息，这些结构提供对传感器的各种属性和功能的访问。

## <a name="in-this-section"></a>本部分内容

|主题|描述|
|---|---|
|[SENSOR_VALUE_PAIR](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_value_pair)|此结构对 "传感器属性" 部分中列出的属性键与每个键表示的数据配对。|
|[SENSOR_COLLECTION_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)|此结构包含每个传感器的所有 SENSOR_VALUE_PAIR 结构的列表。|
|[SENSOR_PROPERTY_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_property_list)|此结构包含每个传感器的所有 SENSOR_VALUE_PAIR 结构的列表。|
|[SENSOR_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_config)|此结构包含传感器驱动程序传递给有关每个传感器的类扩展的信息。|
|[SENSOR_CONTROLLER_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)|此结构包含指向回调函数的指针，该函数必须由驱动程序实现，并传递给要调用的类扩展。|
|SENSOR_DATA|此结构定义了其他传感器用于定义特定于传感器的数据类型的基类型。|
|SENSOR_DEVICE_CAPS|此结构描述传感器组件的功能。|
|SENSOR_DATA_HEADER|此结构包含有关传感器读数的信息。|
|VEC3D|此结构保存用于3D 定位数据的单个数据点。|
|起始|此结构用于表示用于简单三维旋转操作的四维向量。|
|MATRIX3X3|此结构用于表示一般3x3 矩阵。|






