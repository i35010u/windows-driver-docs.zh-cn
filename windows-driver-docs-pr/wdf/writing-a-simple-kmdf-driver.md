---
title: 编写简单的 WDF 驱动程序
description: 本主题介绍编写 Kernel-Mode Driver Framework (KMDF) 驱动程序所需的最少功能。 在 UMDF 版本2中开始编写 User-Mode Driver Framework (UMDF) 驱动程序时，需要使用相同的最小功能。
keywords:
- 内核模式驱动程序 WDK KMDF，编写简单的驱动程序
- KMDF WDK，编写简单的驱动程序
- Kernel-Mode Driver Framework WDK，编写简单的驱动程序
- 基于框架的驱动程序 WDK KMDF，编写简单的驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39bbf50dfb23c523ef39445d1de5007a3ad59090
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833913"
---
# <a name="writing-a-simple-wdf-driver"></a>编写简单的 WDF 驱动程序


本主题介绍编写 Kernel-Mode Driver Framework (KMDF) 驱动程序所需的最少功能。 在 UMDF 版本2中开始编写 User-Mode Driver Framework (UMDF) 驱动程序时，需要使用相同的最小功能。




在创建新的 KMDF 或 UMDF 驱动程序时，必须选择一个不多于 32 个字符的驱动程序名称。 此长度限制在 wdfglobals.h 中定义。 如果你的驱动程序名称超出最大长度，则你的驱动程序将无法加载。

每个基于框架的驱动程序都包含一个 [**DriverEntry**](./driverentry-for-kmdf-drivers.md) 例程和一组事件回调函数，框架在发生特定于对象的事件时将调用该函数。 例如，基于框架的简单驱动程序可能由以下内容组成：

-   [**DriverEntry**](./driverentry-for-kmdf-drivers.md)例程，在加载驱动程序并调用 [**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)时调用。

-   一个 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 事件回调函数，当即插即用 (PnP) 管理器使用与驱动程序支持的硬件 id 匹配的硬件标识符 (ID) 报告设备检测时，框架将调用该函数。

    你可以通过提供一个 INF 文件来指定你的驱动程序支持的硬件 Id，操作系统会在第一次将设备连接到计算机时使用该文件来安装驱动程序。 有关系统如何使用 INF 文件和硬件 Id 的详细信息，请参阅 [安装程序如何选择驱动程序](../install/how-windows-selects-a-driver-for-a-device.md)。

    驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) 为检测到的设备创建框架设备对象。

-   当 i/o 管理器向驱动程序发送 i/o 请求时，框架调用的请求处理程序（如 [*EvtIoDefault*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default) 回调函数）。

    当 i/o 管理器将 i/o 请求发送到你的驱动程序时，框架会将请求放入 i/o 队列，然后通过调用请求处理程序通知你的驱动程序。

    驱动程序必须为每个设备创建至少一个 i/o 队列，以便驱动程序可以接收设备的 i/o 请求。 若要创建 i/o 队列，驱动程序将调用 [**WdfIoQueueCreate**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)，这将创建一个框架队列对象并注册设备的请求处理程序。

有关编写基于框架的驱动程序的详细信息，请参阅 [使用框架开发驱动程序](using-the-framework-to-develop-a-driver.md)。

 

