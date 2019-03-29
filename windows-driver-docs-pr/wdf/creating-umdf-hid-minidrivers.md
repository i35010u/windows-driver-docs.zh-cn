---
title: 创建 WDF HID 微型驱动程序
description: 本主题介绍如何创建使用 Windows 驱动程序框架 (WDF) 人体学接口设备 (HID) 微型驱动程序。
ms.assetid: 4FEDFE4B-F3B2-4B34-80DC-84BFFA4C612B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba6ee6144018d03814bd177d9981d7b758347b32
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577132"
---
# <a name="creating-wdf-hid-minidrivers"></a>创建 WDF HID 微型驱动程序


本主题介绍如何创建使用 Windows 驱动程序框架 (WDF) 人体学接口设备 (HID) 微型驱动程序。

您可以编写使用 KMDF 或 UMDF HID 微型驱动程序。 我们建议从与 vhidmini2 微型驱动程序示例。 您可以编译此示例驱动程序，使用 KMDF 或 UMDF 2.x。

**需要提供哪些**

1.  你将编写下一个较低的筛选器驱动程序*MsHidUmdf.sys* （适用于 UMDF) 或*MsHidKmdf.sys* （适用于 KMDF)，这两者都是作为操作系统的一部分。
2.  下载并查看[vhidmini2 示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/vhidmini2)。

3.  调用[ **WdfFdoInitSetFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff547273)来自驱动程序的[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数。

4.  创建 I/O 队列用于接收 I/O 请求*MsHidUmdf.sys*或*MsHidKmdf.sys*将从类驱动程序传递到您的驱动程序。

5.  提供[ *EvtIoDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541758)分支到特定于 IOCTL 的方法处理程序的回调函数。 查看中所述 Ioctl [WDF HID 微型驱动程序 Ioctl](https://msdn.microsoft.com/library/windows/hardware/hh463977) ，并确保您的驱动程序处理你的设备相关的。
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

这两*MsHidUmdf.sys*并*MsHidKmdf.sys*调用 HID 类驱动程序[ **HidRegisterMinidriver** ](https://msdn.microsoft.com/library/windows/hardware/ff539835)例程，以将注册为实际 HID 微型驱动程序。 虽然这些驱动程序充当设备的功能驱动程序，它们只是 I/O 请求传递的类驱动程序为您的驱动程序 (，因此有时也称为*传递的驱动程序*)。 对于 KMDF 和 UMDF，唯一的组件所提供的是 HID 微型驱动程序，这是较低的筛选器驱动程序位于下传递驱动程序。

|                                                                                     |                                                                                        |
|-------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| UMDF 体系结构                                                                   | KMDF 体系结构                                                                      |
| ![hidumdf.sys 驱动程序堆栈中的位置](images/UMDF-basedHIDMinidrivers.png) | ![mshidkmdf.sys 驱动程序堆栈中的位置](images/Framework-basedHIDMinidrivers.png) |

 

 

 





