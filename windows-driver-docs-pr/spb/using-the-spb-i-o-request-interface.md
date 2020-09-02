---
title: 使用 SPB I/O 请求接口
description: 从 Windows 8 开始，SPB framework 扩展 (SpbCx) 是系统提供的组件，它支持 SPB i/o 请求接口。
ms.assetid: 0A752413-FA0B-4C26-BF6D-19033E07095E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4072eb3737d809eab4f383a68d335e989066f3fc
ms.sourcegitcommit: c766ab74e32eb44795cbbd1a4f352d3a6a9adc14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89389571"
---
# <a name="using-the-spb-io-request-interface"></a>使用 SPB I/O 请求接口

从 Windows 8 开始， [SPB framework 扩展](./spb-framework-extension.md) (SpbCx) 是系统提供的组件，它支持 [SPB i/o 请求接口](/previous-versions/hh698224(v=vs.85))。 SPB 外围设备驱动程序使用此接口将 i/o 请求发送到连接到 i2c、SPI 和其他 [简单外围总线](/previous-versions/hh450903(v=vs.85)) 的设备， (SPBs) 。 通过使标准化 i/o 请求接口可用于各种总线类型，SpbCx 简化了在不同硬件供应商的各种硬件平台和 SPB 控制器中提供对一系列外围设备的驱动程序支持的任务。

如果满足以下条件，则连接到 SPB 的外围设备的硬件供应商可以开发可跨多个总线类型运行的一个设备驱动程序：

- 外围设备必须与这些总线硬件兼容。
- 驱动程序可以在所有这些总线类型上使用相同的设备控制协议。

通过消除外围设备驱动程序的特定于总线的代码，SPB 框架扩展缩短了这些驱动程序的开发时间，并确保了跨受支持的总线类型的更一致的行为。

连接到 SPBs 的外围设备未进行内存映射，并且这些设备的驱动程序无法直接访问这些设备的硬件寄存器。 相反，SPB 外围设备驱动程序必须依赖于 SPB 控制器以串行方式将数据传入和传出设备。 若要请求此类传输，驱动程序必须将 i/o 请求发送到设备。 此 i/o 请求将发送到由 SpbCx 管理的队列。

SpbCx 会 with SPB 控制器驱动程序，用于处理来自驱动程序的 i/o 请求。 SPB 控制器的硬件供应商提供了 SPB 控制器驱动程序来执行特定于控制器硬件的任务。

只有驱动程序才能将 i/o 请求发送到 SPB 控制器的 i/o 请求接口。 应用程序不能直接向 SPB 控制器发送 i/o 请求。 相反，应用程序可以将 i/o 请求发送到与 SPB 连接的外围设备的驱动程序，然后依靠驱动程序向 SPB 控制器发送将数据传输到设备或从设备传输数据所需的任何 i/o 请求。

在驱动程序可以将 i/o 请求发送到使用 SPB 连接的外围设备之前，驱动程序必须打开与设备建立的逻辑连接。 若要打开此连接，驱动程序将使用从即插即用管理器接收为硬件资源的连接 ID。 有关详细信息，请参阅 [SPB 外围设备的连接 id](./connection-ids-for-spb-connected-peripheral-devices.md)。

SpbCx 和 SPB 控制器驱动程序共同处理与 SPB 连接的外围设备的读取和写入请求。 为了响应 [**IRP \_ MJ \_ 读取**](/previous-versions/ff546883(v=vs.85)) 请求，SPB 控制器会将指定数量的字节从外围设备传输到驱动程序提供的缓冲区。 为了响应 [**IRP \_ MJ \_ 写入**](/previous-versions//ff546904(v=vs.85)) 请求，SPB 控制器会将指定数量的字节从驱动程序提供的缓冲区传输到外围设备。

为了使 **IRP \_ mj \_ 读取** 或 **irp \_ mj \_ 写入** 请求传输零字节，SpbCx 完成了状态为 "成功" \_ 状态代码的请求，但不执行任何操作。

SpbCx 和 SPB 控制器驱动程序还处理这些特定于 SPB 的 i/o 控制代码 (IOCTLs) ：

- [**IOCTL \_ SPB \_ 执行 \_ 顺序**](./spb-ioctls.md#ioctl_spb_execute_sequence)
- [**IOCTL \_ SPB \_ 锁定 \_ 控制器**](./spb-ioctls.md#ioctl_spb_lock_controller-control-code)
- [**IOCTL \_ SPB \_ 解锁 \_ 控制器**](./spb-ioctls.md#ioctl_spb_unlock_controller-control-code)

SPB 外设驱动程序使用这些 IOCTLs 执行 *i/o 传输顺序*。 I/o 传输序列是一组有序的总线传输 (读取和写入操作，作为单个原子总线操作执行) 。 有关这些 IOCTLs 的详细信息，请参阅 [I/o 传输序列](./i-o-transfer-sequences.md)。

特定 SPB 控制器的 SPB 控制器驱动程序可能支持执行特定于硬件的函数的自定义 IOCTLs。 这些 IOCTLs 是 SpbCx 不处理的，而 SPB 控制器的硬件供应商却支持需要执行特定于硬件操作的 SPB 外设驱动程序的优点。 如果 SPB 外设驱动程序发送的 IOCTL 既不 SpbCx，也不能识别 SPB 控制器驱动程序，则不执行任何操作，并且 i/o 请求的完成状态的错误状态值为 " \_ 不 \_ 支持"。

与 SPB 连接的外围设备的驱动程序通常是 [用户模式驱动程序框架](../wdf/overview-of-the-umdf.md) (UMDF) 驱动程序或 [内核模式驱动程序框架](../wdf/index.md) (KMDF) 驱动程序。 若要将读取、写入或 IOCTL 请求发送到已连接到 SPB 的外围设备，UMDF 驱动程序会调用方法，例如 [**IWDFIoRequest：： send**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)。 KMDF 驱动程序调用方法，例如 [**WdfIoTargetSendReadSynchronously**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously)、 [**WdfIoTargetSendWriteSynchronously**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendwritesynchronously)或 [**WdfIoTargetSendIoctlSynchronously**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously)。

有关演示如何将 i/o 请求发送到 SPB 连接外围设备的代码示例，请参阅以下主题：

[用户模式 SPB 外设驱动程序的硬件资源](./hardware-resources-for-user-mode-spb-peripheral-drivers.md)

[内核模式 SPB 外设驱动程序的硬件资源](./hardware-resources-for-kernel-mode-spb-peripheral-drivers.md)
