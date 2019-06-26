---
title: 编写简单的 WDF 驱动程序
description: 本主题介绍您需要自己编写的内核模式驱动程序框架 (KMDF) 驱动程序的最少功能。 需要相同的最小功能来编写在 UMDF 版本 2 中启动的用户模式驱动程序框架 (UMDF) 驱动程序。
ms.assetid: 6225b81c-e0da-473a-ba38-24846436dae7
keywords:
- 内核模式驱动程序 WDK KMDF，编写一个简单的驱动程序
- KMDF WDK、 编写简单的驱动程序
- 内核模式驱动程序框架 WDK，编写一个简单的驱动程序
- 基于框架的驱动程序 WDK KMDF，编写一个简单的驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8c5f470d5bb7e60af0acff5f6ac190d55947454
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386114"
---
# <a name="writing-a-simple-wdf-driver"></a>编写简单的 WDF 驱动程序


本主题介绍您需要自己编写的内核模式驱动程序框架 (KMDF) 驱动程序的最少功能。 需要相同的最小功能来编写在 UMDF 版本 2 中启动的用户模式驱动程序框架 (UMDF) 驱动程序。




在创建新的 KMDF 或 UMDF 驱动程序时，必须选择一个不多于 32 个字符的驱动程序名称。 此长度限制在 wdfglobals.h 中定义。 如果驱动程序名称超过了最大长度，您的驱动程序将无法加载。

每个基于 framework 的驱动程序组成[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)例程和一系列事件回叫函数，框架将调用特定于对象的事件发生。 例如，一个简单的基于框架的驱动程序可能包括：

-   一个[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)例程，称为加载驱动程序和其调用[ **WdfDriverCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdrivercreate)。

-   [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)事件回调函数，框架将调用时插即用 (PnP) 管理器报告具有匹配硬件的硬件标识符 (ID) 的设备检测该驱动程序支持的 ID。

    指定硬件驱动程序支持通过提供一个 INF 文件，该操作系统使用其中一个设备连接到的计算机首次安装驱动程序文件的 Id。 有关系统如何使用 INF 文件和硬件 Id 的详细信息，请参阅[安装程序如何选择驱动程序](https://docs.microsoft.com/windows-hardware/drivers/install/how-setup-selects-drivers)。

    在驱动程序[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数调用[ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)若要创建的框架设备对象检测到的设备。

-   一个请求处理程序，如[ *EvtIoDefault* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)框架在 I/O 管理器向驱动程序发送的 I/O 请求时调用的回调函数。

    当 I/O 管理器将 I/O 请求发送到您的驱动程序时，框架将 I/O 队列中放入请求，并随后通知您的驱动程序通过调用请求处理程序。

    该驱动程序必须创建至少一个 I/O 队列用于每个设备，以便该驱动程序可以接收设备的 I/O 请求。 若要创建的 I/O 队列，驱动程序调用[ **WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuecreate)，后者创建 framework 队列对象并注册设备的请求处理程序。

有关编写基于 framework 的驱动程序的详细信息，请参阅[使用框架来开发驱动程序](using-the-framework-to-develop-a-driver.md)。

 

 





