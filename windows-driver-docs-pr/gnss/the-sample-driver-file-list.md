---
title: 地理位置示例驱动程序文件列表
description: 地理位置驱动程序示例的源文件都包含以下类别的文件。
ms.assetid: 8A9A1102-921B-40FF-94F2-FA9E3C1CE662
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ab4fbd174231d4a40c8bf3dcfed7525521165b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568141"
---
# <a name="geolocation-sample-driver-file-list"></a>地理位置示例驱动程序文件列表

> [!IMPORTANT] 
> 已弃用此文档和 Windows 8.1 的地理位置驱动程序示例。

地理位置驱动程序示例的源文件都包含以下类别的文件。

-   共有 UMDF 传感器驱动程序的常规文件。
-   提供用于演示模拟地理位置传感器的支持的特定于传感器的文件。

下表描述共有 UMDF 传感器驱动程序的常规文件。

| 文件名                          | 目录                                                                                                                                                                                                                   |
|------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Device.cpp                         | 包含 CMyDevice 成员函数的实现。 这包括**OnPrepareHardware**方法将创建并初始化传感器类扩展。                                                     |
| Device.h                           | 包含 CMyDevice 类的定义。                                                                                                                                                                             |
| Dllsup.cpp                         | 包含驱动程序 DLL 的入口点 (DLLMain)。                                                                                                                                                                           |
| Driver.cpp                         | 包含 CMyDriver 成员函数的实现。 这包括**OnDeviceAdd**创建 CMyDevice 类的实例方法 （请参阅 Device.cpp 的说明）。                                    |
| Driver.h                           | 包含 CMyDriver 类的定义。                                                                                                                                                                              |
| internal.h                         | 包含的示例驱动程序的本地类型定义。                                                                                                                                                                     |
| makefile.inc                       | 生成所需。INF 文件。                                                                                                                                                                                            |
| Queue.cpp                          | 包含 CMyQueue 成员函数的实现。 这包括**CreateInstance**方法，用于创建设备的 I/O 队列的实例。                                                       |
| Queue.h                            | 包含 CMyQueue 类的定义。                                                                                                                                                                               |
| Resource.h                         | 包含由 SensorsGeolocationSample.h 的定义。                                                                                                                                                               |
| Sensor.cpp                         | 包含 CSensor 成员函数的实现。 这包括返回列表的受支持的属性和数据字段的方法和设置可写属性和数据字段的方法。              |
| Sensor.h                           | 包含 CSensor 类的定义。                                                                                                                                                                                |
| SensDDI.cpp                        | 包含在 CSensorDdi 类 ISensorDriver 回调接口的实现。 传感器类扩展调用此接口可检索受支持的数据，如对象、 属性和事件中的方法。 |
| SensorManager.cpp                  | 包含 CSensorManager 类的实现。 此类中的方法，如名称所示，管理传感器设备： 启动它，停止它，检索设备状态中，依次类推。                        |
| SensorManager.h                    | 包含 CSensorManager 类的定义。                                                                                                                                                                       |
| SensorsGeolocationDriverSample.def | 声明模块参数。                                                                                                                                                                                            |
| SensorsGeolocationDriverSample.htm | 包含的示例驱动程序的高级别说明。                                                                                                                                                                    |
| SensorsGeolocationDriverSample.idl | 包含驱动程序的 COM 组件的必要定义。                                                                                                                                                         |
| SensorsGeolocationDriverSample.inf | 包含 Windows 安装程序需要时在 x86 和 amd64 计算机上安装内置驱动程序的信息。                                                                                                        |
| SensorsGeolocationDriverSample.rc  | 包含该驱动程序要求，如文件类型、 文件描述字符串、 文件版本和原始文件名称的资源定义。                                                                             |
| 源                            | 包含一系列由生成实用程序识别的宏定义                                                                                                                                            |

 

下表列出了支持的模拟地理位置传感器的示例驱动程序支持的文件。

|                 |                                                                                                                                                                             |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 文件名       | 目录                                                                                                                                                                    |
| Geolocation.cpp | 包含 CGeolocation 类的实现。 此类中的方法初始化模拟的传感器，检索可读属性，以及设置可写属性。 |
| Geolocation.h   | 包含 CGeolocation 类的定义                                                                                                                           |

 

## <a name="related-topics"></a>相关主题
[传感器地理位置驱动程序示例](sensors-geolocation-driver-sample.md)  



