---
title: 创建 WDF HID 微型驱动程序
description: 本主题介绍如何创建使用 Windows 驱动程序框架 (WDF) 人体学接口设备 (HID) 微型驱动程序。
ms.assetid: 4FEDFE4B-F3B2-4B34-80DC-84BFFA4C612B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bee581b3b38d3c05b89a513d39fb359f22c81af
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377483"
---
# <a name="creating-wdf-hid-minidrivers"></a>创建 WDF HID 微型驱动程序


本主题介绍如何创建使用 Windows 驱动程序框架 (WDF) 人体学接口设备 (HID) 微型驱动程序。

您可以编写使用 KMDF 或 UMDF HID 微型驱动程序。 我们建议从与 vhidmini2 微型驱动程序示例。 您可以编译此示例驱动程序，使用 KMDF 或 UMDF 2.x。

**需要提供哪些**

1.  你将编写下一个较低的筛选器驱动程序*MsHidUmdf.sys* （适用于 UMDF) 或*MsHidKmdf.sys* （适用于 KMDF)，这两者都是作为操作系统的一部分。
2.  下载并查看[vhidmini2 示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/vhidmini2)。

3.  调用[ **WdfFdoInitSetFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitsetfilter)来自驱动程序的[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数。

4.  创建 I/O 队列用于接收 I/O 请求*MsHidUmdf.sys*或*MsHidKmdf.sys*将从类驱动程序传递到您的驱动程序。

5.  提供[ *EvtIoDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)分支到特定于 IOCTL 的方法处理程序的回调函数。 查看中所述 Ioctl [WDF HID 微型驱动程序 Ioctl](https://docs.microsoft.com/previous-versions/hh463977(v=vs.85)) ，并确保您的驱动程序处理你的设备相关的。
6.  对于 UMDF，如果您的驱动程序枚举通过 ACPI，选择性地启用选择性挂起。 在设备的硬件密钥，添加**EnableDefaultIdleNotificationHandler**子项并将其设置为 1。
7.  对于 UMDF，设置以下[INF 指令](specifying-wdf-directives-in-inf-files.md)WDF 具体*DDInstall* INF 文件的部分：

    -   **UmdfKernelModeClientPolicy**到**AllowKernelModeClients** ，以便可以在堆栈中加载内核模式驱动程序。
    -   **UmdfMethodNeitherAction**到**副本**到进程 Ioctl 的方法允许 UMDF\_这两种类型。
    -   **UmdfFileObjectPolicy**到**AllowNullAndUnknownFileObjects**
    -   **UmdfFsContextUsePolicy**到**CanUseFsContext2**

    例如：

    ```cpp
    [hidumdf.NT.Wdf]
    UmdfKernelModeClientPolicy = AllowKernelModeClients
    UmdfMethodNeitherAction=Copy
    UmdfFileObjectPolicy=AllowNullAndUnknownFileObjects
    UmdfFsContextUsePolicy = CanUseFsContext2
    ```

如果你正在编写适用于 Windows 7 UMDF HID 微型驱动程序，下载[Windows Driver Kit (WDK) 8.1](https://go.microsoft.com/fwlink/p/?LinkId=733614)若要获取的源代码*HidUmdf.sys*。 然后，编写 UMDF 1.11 的驱动程序，并包括*HidUmdf.sys*和 UMDF 1.11 的驱动程序包中。

## <a name="architecture"></a>体系结构


HID 类驱动程序 (*HidClass.sys*) 和该框架提供冲突 WDM 调度例程，以处理某些微型驱动程序 （如插和电源管理请求） 的 I/O 请求。 因此，HID 微型驱动程序不能链接到的类驱动程序和框架。 因此，Microsoft 提供了*MsHidUmdf.sys*并*MsHidKmdf.sys*，这是驻留在类驱动程序微型驱动程序之间的 WDM 驱动程序。

这两*MsHidUmdf.sys*并*MsHidKmdf.sys*调用 HID 类驱动程序[ **HidRegisterMinidriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidport/nf-hidport-hidregisterminidriver)例程，以将注册为实际 HID 微型驱动程序。 虽然这些驱动程序充当设备的功能驱动程序，它们只是 I/O 请求传递的类驱动程序为您的驱动程序 (，因此有时也称为*传递的驱动程序*)。 对于 KMDF 和 UMDF，唯一的组件所提供的是 HID 微型驱动程序，这是较低的筛选器驱动程序位于下传递驱动程序。

|                                                                                     |                                                                                        |
|-------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| UMDF 体系结构                                                                   | KMDF 体系结构                                                                      |
| ![hidumdf.sys 驱动程序堆栈中的位置](images/UMDF-basedHIDMinidrivers.png) | ![mshidkmdf.sys 驱动程序堆栈中的位置](images/Framework-basedHIDMinidrivers.png) |

 

 

 





