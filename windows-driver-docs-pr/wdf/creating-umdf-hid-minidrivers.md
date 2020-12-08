---
title: 创建 WDF HID 微型驱动程序
description: 本主题介绍如何使用 Windows 驱动程序框架 (WDF)  (HID) 微型驱动程序创建人机接口设备。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 720e8d145490dcc3d8a72b59d13e91024cc466f4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828999"
---
# <a name="creating-wdf-hid-minidrivers"></a>创建 WDF HID 微型驱动程序


本主题介绍如何使用 Windows 驱动程序框架 (WDF)  (HID) 微型驱动程序创建人机接口设备。

可以使用 KMDF 或 UMDF 编写 HID 微型驱动程序。 建议从 vhidmini2 微型驱动程序示例开始。 可以使用 KMDF 或 UMDF 2.x 编译此示例驱动程序。

**提供的内容**

1.  你将在 UMDF) *MsHidUmdf.sys* (下编写一个较低的筛选器驱动程序，或在 KMDF (的 *MsHidKmdf.sys*) 中写入，这二者都包含在操作系统中。
2.  下载并查看 [vhidmini2 示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/vhidmini2)。

3.  从驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数调用 [**WdfFdoInitSetFilter**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetfilter) 。

4.  创建 i/o 队列，用于接收 *MsHidUmdf.sys* 或 *MsHidKmdf.sys* 从类驱动程序传递到驱动程序的 i/o 请求。

5.  提供分支到特定于 IOCTL 的方法处理程序的 [*EvtIoDeviceControl*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control) 回调函数。 查看 [WDF HID 微型驱动程序 IOCTLs](/previous-versions/hh463977(v=vs.85)) 中描述的 IOCTLs，并确保你的驱动程序处理设备的相关设备。
6.  对于 UMDF，如果你的驱动程序由 ACPI 枚举，则可以选择启用选择性挂起。 在设备的硬件密钥中，添加 **EnableDefaultIdleNotificationHandler** 子项并将其设置为1。
7.  对于 UMDF，请在 INF 文件的特定于 WDF 的 *DDInstall* 部分中设置以下 [inf 指令](specifying-wdf-directives-in-inf-files.md)：

    -   **UmdfKernelModeClientPolicy** 到 **AllowKernelModeClients** ，以便可以将内核模式直通驱动程序加载到堆栈中。
    -   **UmdfMethodNeitherAction** **复制** 到，以允许 UMDF 处理方法的 IOCTLs，而 \_ 不是类型。
    -   **UmdfFileObjectPolicy** 到 **AllowNullAndUnknownFileObjects**
    -   **UmdfFsContextUsePolicy** 到 **CanUseFsContext2**

    例如：

    ```cpp
    [hidumdf.NT.Wdf]
    UmdfKernelModeClientPolicy = AllowKernelModeClients
    UmdfMethodNeitherAction=Copy
    UmdfFileObjectPolicy=AllowNullAndUnknownFileObjects
    UmdfFsContextUsePolicy = CanUseFsContext2
    ```

如果要编写适用于 Windows 7 的 UMDF HID 微型驱动程序，请下载 [Windows 驱动程序工具包 (WDK) 8.1](../download-the-wdk.md) 获取 *HidUmdf.sys* 的源代码。 然后，写入 UMDF 1.11 驱动程序，并在驱动程序包中包含 *HidUmdf.sys* 和 UMDF 1.11。

## <a name="architecture"></a>体系结构


HID 类驱动程序 (*HidClass.sys*) ，而框架提供了冲突的 WDM 调度例程来处理某些 i/o (请求，例如即插即用和电源管理请求，) 微型驱动程序。 因此，HID 微型驱动程序无法链接到类驱动程序和框架。 因此，Microsoft 提供了 *MsHidUmdf.sys* 和 *MsHidKmdf.sys*，它们是位于类驱动程序和微型驱动程序之间的 WDM 驱动程序。

*MsHidUmdf.sys* 和 *MsHidKmdf.sys* 都调用 HID 类驱动程序的 [**HIDREGISTERMINIDRIVER**](/windows-hardware/drivers/ddi/hidport/nf-hidport-hidregisterminidriver)例程作为实际的 HID 微型驱动程序进行注册。 尽管这些驱动程序充当设备的函数驱动程序，但它们只是将 i/o 请求从类驱动程序传递到驱动程序 (，因此有时称为 *传递驱动程序*) 。 对于 KMDF 和 UMDF，提供的唯一组件是 HID 微型驱动程序，它是位于传递驱动程序下的较低筛选器驱动程序。

**UMDF 体系结构**： KMDF 体系结构

**![ 驱动程序堆栈中 hidumdf.sys 的位置](images/UMDF-basedHIDMinidrivers.png)**： ![ 驱动程序堆栈中 mshidkmdf.sys 的位置](images/Framework-basedHIDMinidrivers.png)


 

