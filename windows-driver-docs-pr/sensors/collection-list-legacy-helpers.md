---
title: 集合列表旧帮助器
description: 集合列表旧帮助程序函数由 v2 传感器驱动程序用来与传感器交互\_集合\_列表结构。
ms.assetid: AD5AB3EE-5AD7-4576-8E8E-3FEA08930DD7
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: d1acced6e3386fea3b3d8691becbe88f5f6b8c31
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519273"
---
# <a name="collection-list-legacy-helpers"></a>集合列表旧帮助器


集合列表旧帮助程序函数的 v2 传感器驱动程序用于与进行交互[**传感器\_集合\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)结构。

传感器设备驱动程序软件接口 (DDSI) 一起使用的帮助器函数。

**注意：** 这些旧集合列表帮助程序函数是特定于体系结构。 因此如果您实现您自己的集合列表帮助器函数，传感器驱动程序必须使用它们跨进程边界传输数据。

**CollectionsListGetMarshalledSize**

通过传感器 DDSI 的使用情况

-   设置主键的值\_传感器\_MaximumDataFieldSize\_字节属性。

-   返回*pSize*值从[EvtSensorGetProperties](https://msdn.microsoft.com/library/windows/hardware/dn957032)。

-   返回*pSize*值从[ *EvtSensorGetDataFieldProperties*](https://msdn.microsoft.com/library/windows/hardware/dn957029)。

-   返回*pSize*值从[ *EvtSensorGetDataThresholds*](https://msdn.microsoft.com/library/windows/hardware/dn957031)。

备注

-   请参阅[**传感器\_集合\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)详细了解*pSize*成员。

-   此外，请参阅[通用传感器属性](common-sensor-properties.md)有关详细信息。

**CollectionsListCopyAndMarshall**

通过传感器 DDSI 的使用情况

-   使用中的集合列表来填充[ *EvtSensorGetProperties*](https://msdn.microsoft.com/library/windows/hardware/dn957032)

-   使用中的集合列表来填充[ *EvtSensorGetDataFieldProperties*](https://msdn.microsoft.com/library/windows/hardware/dn957029)

-   使用中的集合列表来填充[ *EvtSensorGetDataThresholds*](https://msdn.microsoft.com/library/windows/hardware/dn957031)

备注

-   请参阅[**传感器\_集合\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)有关详细信息。

**CollectionsListMarshall**

通过传感器 DDSI 的使用情况

-   返回一个指向集合列表。

备注

-   请参阅[**传感器\_集合\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)有关详细信息。

**CollectionsListGetMarshalledSizeWithoutSerialization**

通过传感器 DDSI 的使用情况

-   报表**主键\_SensorHistory\_MaxSize\_字节**属性。

-   报表**主键\_SensorHistory\_MaximumRecordSize\_字节**属性。

备注

-   请参阅[通用传感器属性](common-sensor-properties.md)有关详细信息。

**CollectionsListUpdateMarshalledPointer**

通过传感器 DDSI 的使用情况

-   将缓冲区传递给传感器驱动程序使用[ *EvtSensorSetDataThresholds*](https://msdn.microsoft.com/library/windows/hardware/dn957039)。

-   将缓冲区传递给驱动程序使用[ *EvtSensorDeviceIoControl*](https://msdn.microsoft.com/library/windows/hardware/dn957028)。

备注

-   请参阅[**传感器\_集合\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)有关详细信息。

## <a name="requirements"></a>要求

|                          |                        |
|--------------------------|------------------------|
| 最低受支持的客户端 | Windows 8.1            |
| 最低受支持的服务器 | Windows Server 2012 R2 |
| 标头                   | Sensorsutils.h         |

 

## <a name="related-topics"></a>相关主题


[帮助器函数的封送处理](marshalling-helper-functions.md)

 

 






