---
title: 驱动程序示例文件列表
description: 以下源文件位于 src\SPB\SpbAccelerometer 文件夹中，用于生成 SpbAccelerometer.sys 和 SpbAccelerometer 文件。
ms.assetid: 48965F7F-1396-4E08-974B-3613684FAA6E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c10a577beadf679909079e9d1a61e614b0cc6557
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968110"
---
# <a name="the-driver-sample-file-list"></a>驱动程序示例文件列表


以下源文件位于 src \\ SPB \\ SpbAccelerometer 文件夹中，用于构建 SpbAccelerometer.sys 和 SpbAccelerometer 文件。

**文件**：说明

**AccelerometerDevice**：用于配置传感器、设置属性和查询数据的设备级别方法。

**Adxl345**：设备的注册集定义并定义

**Clientmanager.swift**：实现驱动程序的客户端跟踪逻辑，包括可设置属性的仲裁。

**设备 .cpp**： WDF PnP 事件回调和 helper 方法

**DllMain**：驱动程序的入口点和用于提供 COM 支持的导出函数

**Driver .cpp**： WDF 驱动程序条目事件回调和 helper 方法

**Internal**：常见包含

**makefile. inc.**：定义自定义生成操作。 包括的转换。INX 文件转换为。INF 文件。

**Queue**： IQueueCallbackDeviceIoControl 的实现。

**ReportManager**：维护驱动程序的报告间隔。

**请求 .idl**：定义用于与传感器设备通信的请求接口。

**SensorDdi**：传感器驱动程序回调接口 ISensorDriver 的实现。

**SensorDevice**：定义传感器 DDI 和传感器设备实现之间的接口。

**源**：列出源文件和生成选项

**源。 dep**：定义生成依赖项

**SpbAccelerometer. asl**：适用于外围设备节点的示例 asl 文件。 它声明 I2C 和 GPIO 中断资源。 请注意，每个宏指定一个 ACPI 路径来描述直接依赖关系。

**SpbAccelerometer**：驱动程序跟踪 GUID 的声明

**SpbAccelerometer**：用于提供 COM 支持的导出函数的声明

**SpbAccelerometer**：驱动程序的库接口文件

**SpbAccelerometer. inx**：描述驱动程序的安装。 生成过程将此转换为 .INF。

**SpbAccelerometer**：资源文件

**SpbRequest**：通过 SPB 实现基于注册的设备访问。

**Trace .h**：设置 WPP 跟踪。


 

## <a name="related-topics"></a>相关主题
[SpbAccelerometer 驱动程序示例](spbaccelerometer-driver-sample.md)  



