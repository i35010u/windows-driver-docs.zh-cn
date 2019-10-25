---
title: 集合列表旧版帮助程序
description: V2 传感器驱动程序使用集合列表旧版 helper 函数与传感器\_集合\_列表结构进行交互。
ms.assetid: AD5AB3EE-5AD7-4576-8E8E-3FEA08930DD7
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 60a02bdabb936e888a00a62258823913f18deebc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842533"
---
# <a name="collection-list-legacy-helpers"></a>集合列表旧版帮助程序


V2 传感器驱动程序使用集合列表旧版 helper 函数与[**传感器\_集合\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)结构进行交互。

Helper 函数与传感器设备驱动程序软件接口（DDSI）一起使用。

**注意：** 这些旧的集合列表 helper 函数是特定于体系结构的。 因此，如果你实现自己的集合列表 helper 函数，则传感器驱动程序不得使用它们来跨进程边界传输数据。

**CollectionsListGetMarshalledSize**

传感器 DDSI 的使用情况

-   设置 PKEY\_传感器\_MaximumDataFieldSize\_Bytes 属性的值。

-   返回[EvtSensorGetProperties](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)中的*pSize*值。

-   返回[*EvtSensorGetDataFieldProperties*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)中的*pSize*值。

-   返回[*EvtSensorGetDataThresholds*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)中的*pSize*值。

备注

-   有关*pSize*成员的详细信息，请参阅[**传感器\_收集\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)。

-   另请参阅[常见传感器属性](common-sensor-properties.md)以了解详细信息。

**CollectionsListCopyAndMarshall**

传感器 DDSI 的使用情况

-   填充 EvtSensorGetProperties 中的集合[列表](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)

-   填充 EvtSensorGetDataFieldProperties 中的集合[列表](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)

-   填充 EvtSensorGetDataThresholds 中的集合[列表](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)

备注

-   有关详细信息，请参阅[**传感器\_收集\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)。

**CollectionsListMarshall**

传感器 DDSI 的使用情况

-   返回指向集合列表的指针。

备注

-   有关详细信息，请参阅[**传感器\_收集\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)。

**CollectionsListGetMarshalledSizeWithoutSerialization**

传感器 DDSI 的使用情况

-   报告**PKEY\_SensorHistory\_MaxSize\_Bytes**属性。

-   报告**PKEY\_SensorHistory\_MaximumRecordSize\_Bytes**属性。

备注

-   有关详细信息，请参阅[常见传感器属性](common-sensor-properties.md)。

**CollectionsListUpdateMarshalledPointer**

传感器 DDSI 的使用情况

-   使用[*EvtSensorSetDataThresholds*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)将缓冲区传递到传感器驱动程序。

-   使用[*EvtSensorDeviceIoControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)将缓冲区传递给驱动程序。

备注

-   有关详细信息，请参阅[**传感器\_收集\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)。

## <a name="requirements"></a>要求

|                          |                        |
|--------------------------|------------------------|
| 最低受支持的客户端 | Windows 8.1            |
| 最低受支持的服务器 | Windows Server 2012 R2 |
| 标头                   | Sensorsutils         |

 

## <a name="related-topics"></a>相关主题


[封送处理 helper 函数](marshalling-helper-functions.md)

 

 






