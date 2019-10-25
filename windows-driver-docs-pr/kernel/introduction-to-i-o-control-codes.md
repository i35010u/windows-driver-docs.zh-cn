---
title: I/O 控制代码简介
description: I/O 控制代码简介
ms.assetid: 8b9e09ef-56f9-42b9-9b65-04bc380f3a1e
keywords:
- I/o 控制代码 WDK 内核，关于 i/o 控制代码
- 控制代码 WDK IOCTLs，关于 i/o 控制代码
- IOCTLs WDK 内核，关于 i/o 控制代码
- 私有 IOCTLs WDK 内核
- 公共 IOCTLs WDK 内核
- IOCTLs WDK 用户模式
- 用户模式组件 WDK IOCTLs
- I/o 控制代码 WDK 用户模式
- 控制代码 WDK 用户模式
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11e88ea3f951dd148e8f69ebee6a3b489ec91c07
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828212"
---
# <a name="introduction-to-io-control-codes"></a>I/O 控制代码简介





I/o 控制代码（IOCTLs）用于在用户模式应用程序和驱动程序之间进行通信，或用于在堆栈中的驱动程序内部进行通信。 I/o 控制代码是使用 Irp 发送的。

用户模式应用程序通过调用[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)将 IOCTLs 发送到驱动程序，如 Microsoft Windows SDK 文档中所述。 调用**DeviceIoControl**会导致 i/o 管理器创建[**IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求并将其发送到最顶层的驱动程序。

此外，上层驱动程序可以通过创建和发送**IRP\_mj\_设备\_控件**或[**irp\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)请求，将 IOCTLs 发送到较低级别的驱动程序。 驱动程序会在[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)和[*DispatchInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中处理这些请求。 （用户模式应用程序无法将**IRP\_MJ 发送\_内部\_设备\_控制**请求。）

有些 IOCTLs 是 "公共的"，而有些则是 "专用"。 公共 IOCTLs 通常由 Microsoft 在 Windows 驱动程序工具包（WDK）或 Windows SDK 中进行系统定义和记录。 它们可以通过用户模式组件对[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)的调用发送，也可以使用 irp 从一个内核模式驱动程序发送到另一个，使用**IRP\_mj\_设备\_控制**或**IRP\_MJ\_内部\_设备\_控制**请求。 公共 IOCTLs 的示例包括[SCSI 端口 I/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)和[I8042prt 鼠标内部设备控制请求](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

另一方面，专用 IOCTLs 旨在由供应商的软件组件专门使用来相互通信。 Private IOCTLs 通常在供应商提供的标头文件中定义，并且未公开记录。 类似于公用 IOCTLs，它们可能通过用户模式组件对[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)的调用发送，也可能通过使用**IRP\_MJ\_设备\_控制**或**IRP\_MJ 发送到另一个内核模式驱动程序\_内部\_设备\_控制**请求。

公有和私有 IOCTLs 的编码没有区别。 不过，可以在供应商定义的 IOCTLs 中使用的内部代码存在差异，与用于系统定义的 IOCTLs 的内部代码不同。 如果可用的公共 IOCTLs 不能满足你的需求，则可以定义新的专用 IOCTLs，你的软件组件可以使用它们互相通信。 有关详细信息，请参阅[定义 I/o 控制代码](defining-i-o-control-codes.md)。

 

 




