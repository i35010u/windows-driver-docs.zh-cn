---
title: 地理位置示例驱动程序文件列表
description: 地理位置驱动程序示例的源文件包括以下类别的文件。
ms.assetid: 8A9A1102-921B-40FF-94F2-FA9E3C1CE662
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73e7f8ccac5fe92c1f0a0d3b5f24ade5c3c2a59c
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968258"
---
# <a name="geolocation-sample-driver-file-list"></a>地理位置示例驱动程序文件列表

> [!IMPORTANT] 
> 此文档和 Windows 8.1 的地理位置驱动程序示例已弃用。

地理位置驱动程序示例的源文件包括以下类别的文件。

-   UMDF 传感器驱动程序公用的常规文件。
-   提供的特定于传感器的文件，用于演示对模拟地理位置传感器的支持。

下表描述了 UMDF 传感器驱动程序所共有的常规文件。

| 文件名                          | 目录                                                                                                                                                                                                                   |
|------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 设备 .cpp                         | 包含 CMyDevice 成员函数的实现。 这包括创建和初始化传感器类扩展的**OnPrepareHardware**方法。                                                     |
| 设备。h                           | 包含 CMyDevice 类的定义。                                                                                                                                                                             |
| Dllsup .cpp                         | 包含驱动程序 DLL 的入口点（DLLMain）。                                                                                                                                                                           |
| 驱动程序 .cpp                         | 包含 CMyDriver 成员函数的实现。 这包括创建 CMyDevice 类的实例的**OnDeviceAdd**方法（请参阅设备的说明）。                                    |
| 驱动程序。h                           | 包含 CMyDriver 类的定义。                                                                                                                                                                              |
| Internal。h                         | 包含示例驱动程序的本地类型定义。                                                                                                                                                                     |
| Makefile                       | 需要生成。INF 文件。                                                                                                                                                                                            |
| Queue                          | 包含 CMyQueue 成员函数的实现。 这包括**CreateInstance**方法，该方法为设备创建 i/o 队列的实例。                                                       |
| Queue。h                            | 包含 CMyQueue 类的定义。                                                                                                                                                                               |
| Resource.h                         | 包含 SensorsGeolocationSample 使用的定义。                                                                                                                                                               |
| 传感器 .cpp                         | 包含 CSensor 成员函数的实现。 这包括返回支持的属性和数据字段的列表以及设置可写属性和数据字段的方法的方法。              |
| 传感器。h                           | 包含 CSensor 类的定义。                                                                                                                                                                                |
| SensDDI .cpp                        | 包含 CSensorDdi 类中的 ISensorDriver 回调接口的实现。 传感器类扩展调用此接口中的方法来检索支持的数据，例如对象、属性和事件。 |
| SensorManager .cpp                  | 包含 CSensorManager 类的实现。 如名称所示，此类中的方法是管理传感器设备：启动、停止、检索设备状态等。                        |
| SensorManager                    | 包含 CSensorManager 类的定义。                                                                                                                                                                       |
| SensorsGeolocationDriverSample | 声明模块参数。                                                                                                                                                                                            |
| SensorsGeolocationDriverSample.htm | 包含示例驱动程序的高级说明。                                                                                                                                                                    |
| SensorsGeolocationDriverSample .idl | 包含驱动程序的 COM 组件所需的定义。                                                                                                                                                         |
| SensorsGeolocationDriverSample .inf | 包含在 x86 和 amd64 计算机上安装内置驱动程序时 Windows 安装程序所需的信息。                                                                                                        |
| SensorsGeolocationDriverSample .rc  | 包含驱动程序所需的资源的定义，例如文件类型、文件描述字符串、文件版本和原始文件名。                                                                             |
| 源                            | 包含一个由生成实用工具识别的宏定义                                                                                                                                            |

 

下表列出了支持示例驱动程序支持的模拟地理位置传感器的文件。

**文件名**：内容

**地理位置 .cpp**：包含 CGeolocation 类的实现。 此类中的方法初始化模拟传感器、检索可读属性并设置可写属性。

**地理位置 .h**：包含 CGeolocation 类的定义


 

## <a name="related-topics"></a>相关主题
[传感器地理位置驱动程序示例](sensors-geolocation-driver-sample.md)  



