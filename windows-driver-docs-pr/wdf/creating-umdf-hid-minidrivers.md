---
title: 创建 WDF HID 微型驱动程序
description: 本主题介绍如何使用 Windows 驱动程序框架（WDF）创建人机接口设备（HID）微型驱动程序。
ms.assetid: 4FEDFE4B-F3B2-4B34-80DC-84BFFA4C612B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 833cd492992c9679a0812d1a5394c3060e7be1cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844676"
---
# <a name="creating-wdf-hid-minidrivers"></a>创建 WDF HID 微型驱动程序


本主题介绍如何使用 Windows 驱动程序框架（WDF）创建人机接口设备（HID）微型驱动程序。

可以使用 KMDF 或 UMDF 编写 HID 微型驱动程序。 建议从 vhidmini2 微型驱动程序示例开始。 可以使用 KMDF 或 UMDF 2.x 编译此示例驱动程序。

**提供的内容**

1.  你将在*MsHidUmdf* （适用于 UMDF）或*MSHIDKMDF* （对于 KMDF）下编写一个较低的筛选器驱动程序，这两个驱动程序都包含在操作系统中。
2.  下载并查看[vhidmini2 示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/vhidmini2)。

3.  从驱动程序的[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数调用[**WdfFdoInitSetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetfilter) 。

4.  创建 i/o 队列，以接收从类驱动程序到驱动程序的*MsHidUmdf*或*MsHidKmdf*传递的 i/o 请求。

5.  提供分支到特定于 IOCTL 的方法处理程序的[*EvtIoDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)回调函数。 查看[WDF HID 微型驱动程序 IOCTLs](https://docs.microsoft.com/previous-versions/hh463977(v=vs.85))中描述的 IOCTLs，并确保你的驱动程序处理设备的相关设备。
6.  对于 UMDF，如果你的驱动程序由 ACPI 枚举，则可以选择启用选择性挂起。 在设备的硬件密钥中，添加**EnableDefaultIdleNotificationHandler**子项并将其设置为1。
7.  对于 UMDF，请在 INF 文件的特定于 WDF 的*DDInstall*部分中设置以下[inf 指令](specifying-wdf-directives-in-inf-files.md)：

    -   **UmdfKernelModeClientPolicy**到**AllowKernelModeClients** ，以便可以将内核模式直通驱动程序加载到堆栈中。
    -   要**复制**到的**UmdfMethodNeitherAction** ，以允许 UMDF 处理方法\_两种类型的 IOCTLs。
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

如果要编写适用于 Windows 7 的 UMDF HID 微型驱动程序，请下载[Windows 驱动程序工具包（WDK） 8.1](https://go.microsoft.com/fwlink/p/?LinkId=733614)以获取*HidUmdf*的源代码。 然后，写入 UMDF 1.11 驱动程序，并在驱动程序包中包含*HidUmdf*和 UMDF 1.11。

## <a name="architecture"></a>体系结构


HID 类驱动程序（*HidClass*）和框架提供了冲突的 WDM 调度例程来处理微型驱动程序的某些 i/o 请求（如即插即用和电源管理请求）。 因此，HID 微型驱动程序无法链接到类驱动程序和框架。 因此，Microsoft 提供了*MsHidUmdf*和*MsHidKmdf*，它们是位于类驱动程序和微型驱动程序之间的 WDM 驱动程序。

*MsHidUmdf*和*MSHIDKMDF*都调用 HID 类驱动程序的[**HidRegisterMinidriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidport/nf-hidport-hidregisterminidriver)例程来注册为实际的 HID 微型驱动程序。 尽管这些驱动程序充当设备的函数驱动程序，但它们只是将来自类驱动程序的 i/o 请求传递到你的驱动程序（因此有时称为*传递驱动程序*）。 对于 KMDF 和 UMDF，提供的唯一组件是 HID 微型驱动程序，它是位于传递驱动程序下的较低筛选器驱动程序。

|                                                                                     |                                                                                        |
|-------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| UMDF 体系结构                                                                   | KMDF 体系结构                                                                      |
| ![驱动程序堆栈中 hidumdf 的位置](images/UMDF-basedHIDMinidrivers.png) | ![驱动程序堆栈中 mshidkmdf 的位置](images/Framework-basedHIDMinidrivers.png) |

 

 

 





