---
title: 使用 SPB I/O 请求接口
description: 从 Windows 8 中，存储框架扩展 (SpbCx) 是支持的存储 I/O 请求接口的系统提供的组件。
ms.assetid: 0A752413-FA0B-4C26-BF6D-19033E07095E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0a007058fb4cb7f59b7c8f03cb4eb8bf747bcd1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383498"
---
# <a name="using-the-spb-io-request-interface"></a>使用 SPB I/O 请求接口

从 Windows 8 开始[存储框架扩展](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-framework-extension)(SpbCx) 是系统提供的组件，它支持[存储 I/O 请求接口](https://docs.microsoft.com/previous-versions/hh698224(v=vs.85))。 存储外围设备驱动程序使用此接口将 I/O 请求发送到设备连接到 I²C、 SPI，和其他[简单的外围总线](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))(SPBs)。 通过在不同的总线类型之间进行标准化的 I/O 请求接口可用，SpbCx 简化了跨各种硬件平台和不同的硬件中的存储控制器为一系列的外围设备提供驱动程序支持的任务供应商。

如果满足以下条件，与存储连接的外围设备的硬件供应商可以开发一个设备驱动程序可以跨多个总线类型工作：

- 外围设备必须是硬件兼容与这些总线。
- 该驱动程序可以跨所有这些总线类型使用相同的设备控制协议。

通过消除外围设备驱动程序的特定于总线的代码，存储框架扩展可以缩短这些驱动程序的开发时间，并在支持的总线类型确保更加一致的行为。

连接到 SPBs 的外围设备不是内存映射，并且这些设备的驱动程序不能直接访问这些设备的硬件寄存器。 相反，存储外围设备驱动程序必须依赖于存储控制器，以按顺序传输设备数据。 若要请求此类传输，该驱动程序必须向设备发送的 I/O 请求。 此 I/O 请求发送到由 SpbCx 管理的队列。

所以，就会以处理来自驱动程序的 I/O 请求的存储控制器驱动程序与协作 SpbCx。 存储控制器的硬件供应商提供的存储控制器驱动程序来执行特定于控制器硬件的任务。

驱动程序可以将 I/O 请求发送到的存储控制器的 I/O 请求接口。 应用程序无法直接将 I/O 请求发送到存储控制器。 相反，应用程序可以将 I/O 请求发送到已连接存储的外围设备中，该驱动程序，然后依赖于要发送到或从设备传输数据时可能需要的任何 I/O 请求的存储控制器的驱动程序。

驱动程序可以将 I/O 请求发送到与存储连接的外围设备之前，该驱动程序必须打开打开到设备的逻辑连接。 若要打开此连接，该驱动程序时，可使用它收到的连接 ID 作为插管理器从一个硬件资源。 有关详细信息，请参阅[存储外围设备的连接 Id](https://docs.microsoft.com/windows-hardware/drivers/spb/connection-ids-for-spb-connected-peripheral-devices)。

SpbCx 和存储控制器驱动程序，共同处理读取和写入存储连接的外围设备的请求。 以响应[ **IRP\_MJ\_读取**](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))请求，存储控制器将指定的字节数从外围设备传输到驱动程序所提供的缓冲区。 以响应[ **IRP\_MJ\_编写**](https://docs.microsoft.com/en-us/previous-versions//ff546904(v=vs.85))请求，存储控制器将指定的字节数从驱动程序所提供的缓冲区传输到外围设备。

有关**IRP\_MJ\_读取**或**IRP\_MJ\_编写**请求将零字节，SpbCx 完成状态请求\_成功状态代码，但不执行任何操作。

SpbCx 和存储控制器驱动程序还可以处理这些特定于存储的 I/O 控制代码 (Ioctl):

- [**IOCTL\_SPB\_EXECUTE\_SEQUENCE**](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-ioctls#ioctl-spb-execute-sequence)
- [**IOCTL\_存储\_锁\_控制器**](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-ioctls#ioctl-spb-lock-controller)
- [**IOCTL\_存储\_解锁\_控制器**](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-ioctls#ioctl_spb_unlock_controller-control-code)

存储外围设备驱动程序将使用这些 Ioctl 执行*I/O 传输序列*。 I/O 传输序列是一组有序的总线传输 （读取和写入操作），作为单个、 原子总线操作执行。 有关这些 Ioctl 的详细信息，请参阅[I/O 传输序列](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences)。

特定的存储控制器的存储控制器驱动程序可能支持自定义 Ioctl 执行特定于硬件的功能。 这些是的 Ioctl SpbCx 不处理并且存储控制器的硬件供应商支持为了方便存储外围设备驱动程序，需要执行特定于硬件的操作。 如果存储外围设备驱动程序发送 SpbCx 和存储控制器驱动程序都不会识别 IOCTL，会执行任何操作和 I/O 请求完成具有状态的错误状态值\_不\_受支持。

与存储连接的外围设备的驱动程序通常是[用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)(UMDF) 驱动程序或[内核模式驱动程序框架](https://docs.microsoft.com/en-us/windows-hardware/drivers/wdf/index)(KMDF) 驱动程序。 若要将读取、 写入或 IOCTL 请求发送到与存储连接的外围设备，UMDF 驱动程序调用的方法如[ **IWDFIoRequest::Send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)。 KMDF 驱动程序调用的方法，如[ **WdfIoTargetSendReadSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously)， [ **WdfIoTargetSendWriteSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendwritesynchronously)，或[**WdfIoTargetSendIoctlSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously)。

代码示例演示如何将 I/O 请求发送到已连接存储的外围设备，请参阅以下主题：

[用户模式下存储外围设备驱动程序的硬件资源](https://docs.microsoft.com/windows-hardware/drivers/spb/hardware-resources-for-user-mode-spb-peripheral-drivers)

[内核模式存储外围设备驱动程序的硬件资源](https://docs.microsoft.com/windows-hardware/drivers/spb/hardware-resources-for-kernel-mode-spb-peripheral-drivers)
