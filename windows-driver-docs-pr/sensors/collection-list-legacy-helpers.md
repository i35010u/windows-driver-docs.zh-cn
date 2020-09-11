---
title: 集合列表旧版帮助程序
description: V2 传感器驱动程序使用集合列表旧版 helper 函数与传感器 \_ 集合列表结构进行交互 \_ 。
ms.assetid: AD5AB3EE-5AD7-4576-8E8E-3FEA08930DD7
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: ceff9d732a55faebd3300390c42969d14e321044
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010583"
---
# <a name="collection-list-legacy-helpers"></a>集合列表旧版帮助程序


V2 传感器驱动程序使用集合列表旧版 helper 函数与 [**传感器 \_ 集合 \_ 列表**](/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list) 结构进行交互。

Helper 函数与传感器设备驱动程序软件接口一起使用 (DDSI) 。

**注意：** 这些旧的集合列表 helper 函数是特定于体系结构的。 因此，如果你实现自己的集合列表 helper 函数，则传感器驱动程序不得使用它们来跨进程边界传输数据。

**CollectionsListGetMarshalledSize**

传感器 DDSI 的使用情况

-   设置 PKEY \_ 传感器 \_ MaximumDataFieldSize Bytes 属性的值 \_ 。

-   返回[EvtSensorGetProperties](/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)中的*pSize*值。

-   返回[*EvtSensorGetDataFieldProperties*](/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)中的*pSize*值。

-   返回[*EvtSensorGetDataThresholds*](/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)中的*pSize*值。

注释

-   有关*pSize*成员的详细信息，请参阅[**传感器 \_ 收集 \_ 列表**](/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)。

-   另请参阅 [常见传感器属性](common-sensor-properties.md) 以了解详细信息。

**CollectionsListCopyAndMarshall**

传感器 DDSI 的使用情况

-   填充 EvtSensorGetProperties 中的集合[ *EvtSensorGetProperties*列表](/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)

-   填充 EvtSensorGetDataFieldProperties 中的集合[ *EvtSensorGetDataFieldProperties*列表](/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)

-   填充 EvtSensorGetDataThresholds 中的集合[ *EvtSensorGetDataThresholds*列表](/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)

注释

-   有关详细信息，请参阅 [**传感器 \_ 收集 \_ 列表**](/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list) 。

**CollectionsListMarshall**

传感器 DDSI 的使用情况

-   返回指向集合列表的指针。

注释

-   有关详细信息，请参阅 [**传感器 \_ 收集 \_ 列表**](/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list) 。

**CollectionsListGetMarshalledSizeWithoutSerialization**

传感器 DDSI 的使用情况

-   报告 **PKEY \_ SensorHistory \_ MaxSize \_ Bytes** 属性。

-   报告 **PKEY \_ SensorHistory \_ MaximumRecordSize \_ Bytes** 属性。

注释

-   有关详细信息，请参阅 [常见传感器属性](common-sensor-properties.md) 。

**CollectionsListUpdateMarshalledPointer**

传感器 DDSI 的使用情况

-   使用 [*EvtSensorSetDataThresholds*](/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)将缓冲区传递到传感器驱动程序。

-   使用 [*EvtSensorDeviceIoControl*](/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)将缓冲区传递给驱动程序。

注释

-   有关详细信息，请参阅 [**传感器 \_ 收集 \_ 列表**](/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list) 。

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 8。1

**支持的最低服务器**： Windows Server 2012 R2

**标头**： Sensorsutils


 

## <a name="related-topics"></a>相关主题


[帮助程序函数的封送处理](marshalling-helper-functions.md)

 

