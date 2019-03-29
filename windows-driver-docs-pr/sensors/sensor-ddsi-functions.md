---
title: 传感器 DDSI 函数
description: 传感器设备驱动程序软件接口 (DDSI) 函数表示传感器驱动程序将使用此类扩展与之交互的接口。
ms.assetid: 3DB30155-8DBE-4AE9-A0CC-8089DC255E32
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0afbf379b21e98378e19cf552ca99cffa61b5a70
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563773"
---
# <a name="sensor-ddsi-functions"></a>传感器 DDSI 函数

传感器设备驱动程序软件接口 (DDSI) 函数表示传感器驱动程序将使用此类扩展与之交互的接口。 这些函数的实现的类扩展。

## <a name="in-this-section"></a>本节内容

|主题|描述|
|---|---|
|SensorsCxDeviceInitConfig|此函数将配置传感器设备。|
|SensorsCxDeviceInitialize|此函数将初始化传感器类扩展中。|
|SensorsCxSensorCreate|此函数创建实例的传感器类扩展中。|
|SensorsCxSensorInitialize|此函数设置传感器的枚举属性。|
|SensorsCxSensorDataReady|此函数会通知类扩展驱动程序已检索数据。|
|SensorsCxStateChange|用于初始化状态更改。|
|SensorsCxDeviceGetSensorList|此函数返回与 WDFDEVICE 相关联的传感器实例的列表。|
