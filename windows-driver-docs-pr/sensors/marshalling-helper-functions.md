---
title: 帮助程序函数的封送处理
description: 本主题提供有关 sensorsutils 标头文件中的封送处理 helper 函数的信息。
ms.assetid: AE5C70E4-1971-4BAF-AE7D-315A15F030DD
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: d3719233c806d0f5d81d639e90235bd96d30a82a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842449"
---
# <a name="marshalling-helper-functions"></a>帮助程序函数的封送处理


本主题提供有关*sensorsutils*标头文件中的封送处理 helper 函数的信息。

这些帮助程序函数由 v2 传感器驱动程序使用，并与传感器设备驱动程序软件接口（DDSI）一起使用。

如果实现自己的封送处理 helper 函数，请记住，在[ **\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_config)结构中填充传感器的枚举列表时，或使用[**SensorsCxSensorDataReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensordataready)函数报告更新的数据时，不得使用 helper 函数。

## <a name="in-this-section"></a>本部分内容


|主题|描述|
|--|--|
|[时间戳帮助程序](timestamp-helper.md)|时间戳 helper 函数由 v2 传感器驱动程序使用，并用于传感器设备驱动程序软件接口（DDSI）。|
|[PropVariant 帮助程序](propvariant-helpers.md)|V2 传感器驱动程序使用 PropVariant helper 函数操作与传感器关联的[PropVariant](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)结构。|
|[集合列表帮助程序](collection-list-helpers.md)|V2 传感器驱动程序使用集合列表 helper 函数来处理[SENSOR_COLLECTION_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)结构。|
|[集合列表序列化帮助程序](collection-list-serialization-helpers.md)|V2 传感器驱动程序使用集合列表序列化帮助器函数来执行对[SENSOR_COLLECTION_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)结构的序列化相关操作。|
|[集合列表旧帮助程序](collection-list-legacy-helpers.md)|V2 传感器驱动程序使用集合列表旧 helper 函数与[SENSOR_COLLECTION_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)结构进行交互。|

 

## <a name="requirements"></a>要求


**标头：** Sensorsutils

 

 





