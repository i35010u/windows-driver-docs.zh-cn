---
title: 传感器 DDSI 回调
description: 传感器设备驱动程序软件接口 (DDSI) 函数表示传感器驱动程序将使用此类扩展与之交互的接口。
ms.assetid: 3DB30155-8DBE-4AE9-A0CC-8089DC255E32
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6201e6ab3671aad57b0df150c075eef11b0075e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368883"
---
# <a name="sensor-ddsi-callbacks"></a>传感器 DDSI 回调

传感器设备驱动程序软件接口 (DDSI) 函数表示传感器驱动程序将使用此类扩展与之交互的接口。 由传感器驱动程序实现并由类扩展调用这些回调。 您可以找到详细信息中的这些回调[_SENSOR_CONTROLLER_CONFIG 结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)。

## <a name="callbacks"></a>回调

|主题|描述|
|---|---|
|EvtSensorDisableWake|若要禁用唤醒传感器的回调。 |
|EvtSensorEnableWake|若要启用传感器的唤醒的回调。|
|EvtSensorStartStateChangeNotification|用于启动状态更改通知。|
|EvtSensorStopStateChangeNotification|用于停止的状态更改通知。|
|EvtSensorStart|此回调函数启动基于该驱动程序，由指定的默认属性的传感器或设置此类扩展属性。|
|EvtSensorStop|此回调函数停止传感器。|
|EvtSensorGetSupportedDataFields|此回调函数返回由指定的传感器支持的数据字段的列表。|
|EvtSensorGetProperties|此回调函数返回给定传感器的属性。|
|EvtSensorGetDataFieldProperties|此回调函数返回与传感器相关联的给定的数据字段的属性。|
|EvtSensorGetDataInterval|此回调函数返回指定的传感器的数据间隔。|
|EvtSensorSetDataInterval|此回调函数将指定的传感器的数据间隔。|
|EvtSensorGetDataThresholds|此回调函数返回与传感器相关联的阈值。|
|EvtSensorSetDataThresholds|此回调函数设置的阈值与传感器相关联的一个或多个数据字段。|
|EvtSensorDeviceIoControl|此回调函数处理 Ioctl 外部类扩展。|
|EvtSensorSetBatchLatency|此回调函数将指定的传感器的批处理延迟。|

