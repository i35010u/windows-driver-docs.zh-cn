---
title: I/O 控制代码简介
description: I/O 控制代码简介
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
ms.openlocfilehash: 29edd706d2519c792c510acb3336411b629309f2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837235"
---
# <a name="introduction-to-io-control-codes"></a>I/O 控制代码简介





I/o 控制代码 (IOCTLs) 用于用户模式应用程序和驱动程序之间的通信，或用于在堆栈中的驱动程序内部进行通信。 I/o 控制代码是使用 Irp 发送的。

用户模式应用程序通过调用 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)将 IOCTLs 发送到驱动程序，如 Microsoft Windows SDK 文档中所述。 调用 **DeviceIoControl** 会导致 i/o 管理器创建 [**IRP \_ MJ \_ 设备 \_ 控制**](./irp-mj-device-control.md) 请求并将其发送到最顶层的驱动程序。

此外，上层驱动程序可以通过创建和发送 **irp \_ mj \_ 设备 \_ 控制** 或 [**IRP \_ Mj \_ 内部 \_ 设备 \_ 控制**](./irp-mj-internal-device-control.md) 请求，将 IOCTLs 发送到较低级别的驱动程序。 驱动程序会在 [*DispatchDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 和 [*DispatchInternalDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中处理这些请求。  (用户模式应用程序无法发送 **IRP \_ MJ \_ 内部 \_ 设备 \_ 控制** 请求。 ) 

有些 IOCTLs 是 "公共的"，而有些则是 "专用"。 公共 IOCTLs 通常由 Microsoft 在 Windows 驱动程序工具包 (WDK) 或 Windows SDK 中进行系统定义和记录。 它们可以通过用户模式组件对 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)的调用发送，也可以使用 **irp \_ Mj \_ 设备 \_ 控制** 或 **irp \_ mj \_ 内部 \_ 设备 \_ 控制** 请求从一个内核模式驱动程序发送到另一个。 公共 IOCTLs 的示例包括 [SCSI 端口 I/o 控制代码](/windows-hardware/drivers/ddi/index) 和 [I8042prt 鼠标内部设备控制请求](/windows-hardware/drivers/ddi/index)。

另一方面，专用 IOCTLs 旨在由供应商的软件组件专门使用来相互通信。 Private IOCTLs 通常在供应商提供的标头文件中定义，并且未公开记录。 类似于公用 IOCTLs，它们可能通过用户模式组件对 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)的调用发送，也可能使用 **irp \_ Mj \_ 设备 \_ 控制** 或 **irp \_ mj \_ 内部 \_ 设备 \_ 控制** 请求从一个内核模式驱动程序发送到另一个。

公有和私有 IOCTLs 的编码没有区别。 不过，可以在供应商定义的 IOCTLs 中使用的内部代码存在差异，与用于系统定义的 IOCTLs 的内部代码不同。 如果可用的公共 IOCTLs 不能满足你的需求，则可以定义新的专用 IOCTLs，你的软件组件可以使用它们互相通信。 有关详细信息，请参阅 [定义 I/o 控制代码](defining-i-o-control-codes.md)。

 

