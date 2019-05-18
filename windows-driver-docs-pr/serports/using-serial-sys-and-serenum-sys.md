---
title: 使用 Serial.sys 和 Serenum.sys
description: 使用 Serial.sys 和 Serenum.sys
ms.assetid: 2dcf22c8-0666-4b58-8fd3-97a4d17eaa2a
keywords:
- WDK 的串行端口
- 串行设备 WDK
- WDK，串行端口
- 通用的异步接收方发射机 WDK 串行设备
- UART WDK 串行设备
- 功能的驱动程序 WDK 串行端口
- 串行驱动程序 WDK
- 16550 UART 兼容接口 WDK 串行设备
- 较低级别设备筛选器驱动程序 WDK 串行设备
- 更高级别的设备筛选器驱动程序 WDK 串行设备
- 筛选器驱动程序 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4da40df971ff1b17511de0867af86b6a848debde
ms.sourcegitcommit: 6a0636c33e28ce2a9a742bae20610f0f3435262c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2019
ms.locfileid: "65836266"
---
# <a name="using-serialsys-and-serenumsys"></a>使用 Serial.sys 和 Serenum.sys

以下系统组件是可与串行控制器设备具有与 16550 通用异步收发-器 (UART) 兼容的硬件接口一起使用：

-   序列和 Serenum 驱动程序

    Serial.sys （序列） 是串行设备的系统提供的函数驱动程序。 此外可以为任何类型的需要 16550 UART 兼容接口的插设备作为较低级别设备筛选器驱动程序使用序列。

    Serenum.sys (Serenum) 是可以在 RS-232 端口与序列 （或供应商提供的函数驱动程序） 来提供插总线驱动程序功能结合使用的系统提供高级别的设备筛选器驱动程序。

    有关序列和 Serenum 的操作的详细信息，请参阅以下主题：

    - [串行控制器驱动程序概述](serial-drivers-overview.md)
    - [序列和 Serenum 的功能](features-of-serial-and-serenum.md)
    - [串行设备和驱动程序的配置](configuration-of-serial-devices-and-drivers.md)
    - [Serenum 和序列的操作](operation-of-serenum-and-serial.md)
    - [用于 Serial 注册表设置](registry-settings-for-serial.md)
    - [Serenum 的注册表设置](registry-settings-for-serenum.md)
    - [串行驱动程序参考](https://msdn.microsoft.com/library/windows/hardware/ff547476)
    - [Serenum 驱动程序参考](https://msdn.microsoft.com/library/windows/hardware/ff547040)
    - WDK 中 Ntddser.h 标头文件中的数据定义。

<!-- -->

- 端口[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)

    端口类包括*串行端口*并*COM 端口*。 串行端口处于 16550 UART 或兼容的设备上的串行通信硬件接口。 一台计算机上的 RS-232 端口通常是 DB 9 或通过电气连接到串行端口上 UART DB 25 连接器。 COM 端口是符合其他特定于 Windows 的要求的串行端口。 有关详细信息，请参阅[配置的 COM 端口](configuration-of-com-ports.md)。

- COM 端口[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)

    必须使用 COM 端口设备接口来访问 COM 端口。 (有关 COM 端口设备接口类的 GUID 是[ **GUID\_DEVINTERFACE\_COMPORT**](https://msdn.microsoft.com/library/windows/hardware/ff545821)。)

- [COM 端口数据库](com-port-database.md)和[COM 端口数据库支持例程](https://msdn.microsoft.com/library/windows/hardware/ff546483)

    COM 端口数据库对话 COM 端口号的 COM 端口的使用。

有关安装串行设备的信息，请参阅[安装串行设备](installing-serial-devices.md)。

有关串行设备的高级操作的常规信息，请参阅支持的 Microsoft Windows SDK 中的 Windows 基本服务的通信资源有关的信息。

## <a name="serial-driver-samples"></a>串行驱动程序示例

这些示例演示了串行驱动程序。

- [串行](https://go.microsoft.com/fwlink/p/?LinkId=617962)示例生成串行设备功能驱动程序。
- [Serenum](https://go.microsoft.com/fwlink/p/?LinkId=617961)示例提供了一个 RS-232 端口的总线驱动程序的插功能。
- 简单虚拟串行驱动程序 (ComPort) 和控制器的无调制解调器驱动程序 (FakeModem)。
    -   [虚拟串行驱动程序示例 (UMDF 1.0)](https://go.microsoft.com/fwlink/p/?LinkId=617963)
    -   [虚拟 serial2 驱动程序示例 (KMDF)](https://go.microsoft.com/fwlink/p/?LinkId=722209)
