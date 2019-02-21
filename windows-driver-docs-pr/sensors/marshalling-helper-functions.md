---
title: 帮助器函数的封送处理
description: 本主题提供有关封送处理 sensorsutils.h 标头文件中的帮助器函数的信息。
ms.assetid: AE5C70E4-1971-4BAF-AE7D-315A15F030DD
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1d2af831155fcea2123eaa6221471921d812399a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541443"
---
# <a name="marshalling-helper-functions"></a>帮助器函数的封送处理


本主题提供有关在封送处理的帮助器函数的信息*sensorsutils.h*标头文件。

V2 传感器驱动程序，使用这些帮助器函数和传感器设备驱动程序软件接口 (DDSI) 以及使用它们。

如果您实现您自己封送处理的帮助器函数，请记住填充的枚举列表中时，必须不使用 helper 函数[**传感器\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_config)结构，或当报告更新的数据与[ **SensorsCxSensorDataReady** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/nf-sensorscx-sensorscxsensordataready)函数。

## <a name="in-this-section"></a>本部分内容


|主题|描述|
|--|--|
|[时间戳帮助程序](timestamp-helper.md)|时间戳帮助程序函数由 v2 传感器驱动程序，并且与传感器设备驱动程序软件接口 (DDSI) 一起使用。|
|[PropVariant 帮助程序](propvariant-helpers.md)|PropVariant 帮助器函数用于处理由 v2 传感器驱动程序[PROPVARIANT](https://msdn.microsoft.com/library/windows/desktop/aa380072.aspx)与传感器相关联的结构。|
|[集合列表帮助器](collection-list-helpers.md)|集合列表帮助程序函数的 v2 传感器驱动程序，用来处理[SENSOR_COLLECTION_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)结构。|
|[集合列表序列化帮助器](collection-list-serialization-helpers.md)|集合列表序列化帮助器函数用于 v2 传感器驱动程序，对执行序列化相关的操作[SENSOR_COLLECTION_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)结构。|
|[集合列表旧帮助器](collection-list-legacy-helpers.md)|集合列表旧帮助程序函数的 v2 传感器驱动程序用于与进行交互[SENSOR_COLLECTION_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)结构。|

 

## <a name="requirements"></a>要求


**标头：** Sensorsutils.h

 

 





