---
title: I/O 控制代码简介
description: I/O 控制代码简介
ms.assetid: 8b9e09ef-56f9-42b9-9b65-04bc380f3a1e
keywords:
- I/O 控制代码 WDK 内核，有关 I/O 控制代码
- 控制代码 WDK Ioctl 有关 I/O 控制代码
- Ioctl WDK 内核，有关 I/O 控制代码
- 专用 Ioctl WDK 内核
- 公共 Ioctl WDK 内核
- Ioctl WDK 用户模式
- 用户模式组件 WDK Ioctl
- I/O 控制代码 WDK 用户模式
- 控制代码 WDK 用户模式
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82a87e9a5bf437fe01cfcc33487064643bc78e10
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369733"
---
# <a name="introduction-to-io-control-codes"></a>I/O 控制代码简介





I/O 控制代码 (Ioctl) 用于用户模式应用程序和驱动程序之间的通信或在内部在堆栈中的驱动程序之间进行通信。 使用 Irp 发送 I/O 控制代码。

用户模式应用程序通过调用向驱动程序发送 Ioctl [ **DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)，Microsoft Windows SDK 文档中所述。 调用**DeviceIoControl**会导致 I/O 管理器来创建[ **IRP\_MJ\_设备\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求并将其发送到最顶层的驱动程序。

此外，较高级别驱动程序可以将 Ioctl 发送到较低级别的驱动程序通过创建并发送**IRP\_MJ\_设备\_控制**或[ **IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)请求。 驱动程序处理这些请求中的[ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)并[ *DispatchInternalDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。 (用户模式应用程序不能发送**IRP\_MJ\_内部\_设备\_控制**请求。)

某些 Ioctl 是"public"，一些是"私有"。 公共 Ioctl 通常系统定义并由 Microsoft、 Windows Driver Kit (WDK) 或 Windows SDK 中所述。 它们可能会通过对用户模式组件的调用发送[ **DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)，或它们可能会发送从一个内核模式驱动程序到另一种，使用**IRP\_MJ\_设备\_控制**或**IRP\_MJ\_内部\_设备\_控件**请求。 都属于公共 Ioctl [SCSI 端口 I/O 控制代码](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)并[I8042prt 鼠标内部设备控制请求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

专用 Ioctl，另一方面，是为了以独占方式由供应商的软件组件使用与彼此进行通信。 专用 Ioctl 通常在供应商提供的标头文件中定义，且未公开记录。 等公共 Ioctl，它们可能会发送到用户模式组件的调用通过[ **DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)，或它们可能会发送从一个内核模式驱动程序到另一种，使用**IRP\_MJ\_设备\_控件**或**IRP\_MJ\_内部\_设备\_控件**请求。

编码的公钥和私钥 Ioctl 之间没有差异。 有，但是，可以在供应商定义的 Ioctl，与使用的系统定义 Ioctl 比较中使用的内部代码之间的差异。 如果可用的公共 Ioctl 不适合您的需要，可以定义你的软件组件可用于相互通信的新专用 Ioctl。 有关详细信息，请参阅[定义的 I/O 控制代码](defining-i-o-control-codes.md)。

 

 




