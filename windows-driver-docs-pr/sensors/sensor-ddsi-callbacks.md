---
title: 传感器 DDSI 回调
description: 传感器设备驱动程序软件接口（DDSI）函数表示传感器驱动程序用来与类扩展交互的接口。
ms.assetid: 3DB30155-8DBE-4AE9-A0CC-8089DC255E32
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: ae44c084db096b80be45790ccac74c1c4cb661ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845502"
---
# <a name="sensor-ddsi-callbacks"></a>传感器 DDSI 回调

传感器设备驱动程序软件接口（DDSI）函数表示传感器驱动程序用来与类扩展交互的接口。 这些回调由传感器驱动程序实现，由类扩展调用。 可以在[_SENSOR_CONTROLLER_CONFIG 结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)中找到有关这些回调的详细信息。

## <a name="callbacks"></a>回电

|主题|描述|
|---|---|
|EvtSensorDisableWake|用于禁用传感器唤醒的回叫。 |
|EvtSensorEnableWake|用于启用传感器唤醒的回调。|
|EvtSensorStartStateChangeNotification|用于启动状态更改通知。|
|EvtSensorStopStateChangeNotification|用于停止状态更改通知。|
|EvtSensorStart|此回调函数基于驱动程序指定的默认属性或由类扩展设置的属性来启动传感器。|
|EvtSensorStop|此回调函数停止传感器。|
|EvtSensorGetSupportedDataFields|此回调函数返回指定传感器支持的数据字段列表。|
|EvtSensorGetProperties|此回调函数返回给定传感器的属性。|
|EvtSensorGetDataFieldProperties|此回调函数返回与传感器关联的给定数据字段的属性。|
|EvtSensorGetDataInterval|此回调函数返回指定传感器的数据间隔。|
|EvtSensorSetDataInterval|此回调函数设置指定传感器的数据间隔。|
|EvtSensorGetDataThresholds|此回调函数返回与传感器关联的阈值。|
|EvtSensorSetDataThresholds|此回调函数设置与传感器关联的一个或多个数据字段的阈值。|
|EvtSensorDeviceIoControl|此回调函数在类扩展外处理 IOCTLs。|
|EvtSensorSetBatchLatency|此回调函数为指定的传感器设置批处理滞后时间。|

