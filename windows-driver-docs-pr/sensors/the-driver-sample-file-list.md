---
title: 驱动程序示例文件列表
description: 以下源文件 src\SPB\SpbAccelerometer 文件夹中，用于生成 SpbAccelerometer.sys 和 SpbAccelerometer.inf 文件。
ms.assetid: 48965F7F-1396-4E08-974B-3613684FAA6E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92ecbd4aaadc85fee58e387c3d226e895d067708
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525651"
---
# <a name="the-driver-sample-file-list"></a>驱动程序示例文件列表


以下源文件位于 src\\存储\\SpbAccelerometer 文件夹，用于生成 SpbAccelerometer.sys 和 SpbAccelerometer.inf 文件。

|                         |                                                                                                                                                                          |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 文件                    | 描述                                                                                                                                                              |
| AccelerometerDevice.cpp | 配置传感器、 设置属性和查询数据的设备级方法。                                                                                                |
| Adxl345.h               | 设备的注册集定义和定义                                                                                                                             |
| ClientManager.cpp       | 实现驱动程序的客户端跟踪逻辑，包括可设置的属性的约束性仲裁。                                                                             |
| Device.cpp              | WDF 即插即用事件回叫和帮助器方法                                                                                                                               |
| DllMain.cpp             | 驱动程序的入口点和提供 COM 支持的导出的函数                                                                                                    |
| Driver.cpp              | WDF 驱动程序条目事件的回调和帮助器方法                                                                                                                      |
| internal.h              | 常见包括                                                                                                                                                          |
| makefile.inc            | 定义自定义生成操作。 包括的转换。到 INX 文件。INF 文件。                                                                                 |
| Queue.cpp               | IQueueCallbackDeviceIoControl 的实现。                                                                                                                         |
| ReportManager.cpp       | 维护驱动程序的报表时间间隔。                                                                                                                                  |
| Request.idl             | 定义用于与传感器设备通信的请求接口。                                                                                                  |
| SensorDdi.cpp           | 传感器驱动程序回调接口，ISensorDriver 的实现。                                                                                                   |
| SensorDevice.idl        | 定义在传感器 DDI 和传感器设备实现之间的接口。                                                                                      |
| 源                 | 列表源文件和生成选项                                                                                                                                     |
| sources.dep             | 定义生成依赖项                                                                                                                                               |
| SpbAccelerometer.asl    | 外围设备节点的示例 ASL 文件。 它会声明 I2C 和 GPIO 中断资源。 请注意，每个宏指定的 ACPI 路径来描述直接依赖项。 |
| SpbAccelerometer.ctl    | 驱动程序的声明的跟踪的 GUID                                                                                                                                     |
| SpbAccelerometer.def    | 提供 COM 支持的导出函数的声明                                                                                                              |
| SpbAccelerometer.idl    | 驱动程序库接口文件                                                                                                                                          |
| SpbAccelerometer.inx    | 介绍驱动程序的安装。 生成过程将转换成。 INF。                                                                                   |
| SpbAccelerometer.rc     | 资源文件                                                                                                                                                            |
| SpbRequest.cpp          | 通过存储基于注册的设备访问的实现。                                                                                                                |
| Trace.h                 | 设置了 WPP 跟踪。                                                                                                                                                     |

 

## <a name="related-topics"></a>相关主题
[SpbAccelerometer 驱动程序示例](spbaccelerometer-driver-sample.md)  



