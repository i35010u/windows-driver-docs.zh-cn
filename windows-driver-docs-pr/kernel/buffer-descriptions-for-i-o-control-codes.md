---
title: I/O 控制代码的缓冲区说明
description: I/O 控制代码的缓冲区说明
ms.assetid: a458f3fb-a6c7-42ae-870e-1617a96b496f
keywords:
- I/o 控制代码 WDK 内核，缓冲区描述
- 控制代码 WDK IOCTLs，缓冲区说明
- IOCTLs WDK 内核，缓冲区说明
- 缓冲区说明 WDK IOCTLs
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84129ddb9616d0e962c455b9bde9fc8408be9244
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188061"
---
# <a name="buffer-descriptions-for-io-control-codes"></a>I/O 控制代码的缓冲区说明





I/o 控制代码包含在 [**irp \_ mj \_ 设备 \_ 控制**](./irp-mj-device-control.md) 和 [**irp \_ mj \_ 内部 \_ 设备 \_ 控制**](./irp-mj-internal-device-control.md) 请求中。 由于对 Microsoft Windows SDK 文档) 和[**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)中所述的[**DeviceIoControl**](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) (的调用，i/o 管理器将创建这些请求。

因为 [**DeviceIoControl**](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) 和 **IoBuildDeviceIoControlRequest** 同时接受输入缓冲区和输出缓冲区作为参数，所以所有 **IRP \_ mj \_ 设备 \_ 控制** 和 **IRP \_ mj \_ 内部 \_ 设备 \_ 控制** 请求都提供输入缓冲区和输出缓冲区。 系统描述这些缓冲区的方式取决于数据传输类型。 传输类型由创建 IOCTL 代码值的[**CTL \_ 代码**](defining-i-o-control-codes.md)宏中的*TransferType*值指定。

系统说明每个 *TransferType* 值的缓冲区，如下所示：

<a href="" id="method-buffered"></a>方法 \_ 缓冲  
对于此传输类型，Irp 提供指向 **Irp &gt;AssociatedIrp.SystemBuffer**的缓冲区的指针。 此缓冲区表示在对 [**DeviceIoControl**](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) 和 **IoBuildDeviceIoControlRequest**的调用中指定的输入缓冲区和输出缓冲区。 该驱动程序会将数据传入或传出此缓冲区。

对于输入数据，缓冲区大小由驱动程序的[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构中的**DeviceIoControl. InputBufferLength**指定。 对于输出数据，缓冲区大小由驱动程序的**IO \_ 堆栈 \_ 位置**结构中的**DeviceIoControl. OutputBufferLength**指定。

系统为单个输入/输出缓冲区分配的空间大小是两个长度值中较大的一个。

<a href="" id="method-in-direct-or-method-out-direct"></a>\_ \_ 直接或方法 \_ OUT \_ 直接的方法  
对于这些传输类型，Irp 提供指向 **Irp &gt;AssociatedIrp.SystemBuffer**的缓冲区的指针。 这表示对 **DeviceIoControl** 和 **IoBuildDeviceIoControlRequest**的调用中指定的缓冲区。 缓冲区大小由驱动程序的**IO \_ 堆栈 \_ 位置**结构中的**DeviceIoControl. InputBufferLength**指定。

对于这些传输类型，Irp 还会在 ** &gt; MdlAddress**中提供指向 MDL 的指针。 这表示对 [**DeviceIoControl**](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) 和 **IoBuildDeviceIoControlRequest**的调用中指定的缓冲区。 此缓冲区可用作输入缓冲区或输出缓冲区，如下所示：

-   \_ \_ 如果处理 IRP 的驱动程序在调用缓冲区时接收数据，则指定 DIRECT 中的方法。 MDL 描述了一个输入缓冲区，并直接指定了方法，以 \_ \_ 确保执行线程具有对缓冲区的读取访问权限。

-   \_ \_ 如果处理 irp 的驱动程序在完成 irp 之前将数据写入缓冲区，则指定方法 OUT DIRECT。 MDL 描述了输出缓冲区，并指定方法 \_ OUT \_ 直接确保执行线程对缓冲区具有写入访问权限。

对于这两种传输类型， **DeviceIoControl. OutputBufferLength** 指定 MDL 描述的缓冲区大小。

<a href="" id="method-neither"></a>方法 \_ 都不是  
I/o 管理器不提供任何系统缓冲区或 MDLs。 IRP 提供指定给 **DeviceIoControl** 或 **IoBuildDeviceIoControlRequest**的输入和输出缓冲区的用户模式虚拟地址，而无需对其进行验证或映射。

输入缓冲区的地址由驱动程序的**IO \_ 堆栈 \_ 位置**结构中的**DeviceIoControl. Type3InputBuffer**提供，并由**Irp- &gt; UserBuffer**指定输出缓冲区的地址。

缓冲区大小由驱动程序的**IO \_ 堆栈 \_ 位置****结构中的**InputBufferLength 和**DeviceIoControl**提供。

有关 **CTL \_ 代码** 宏以及上面列出的传输类型的详细信息，请参阅 [定义 i/o 控制代码](defining-i-o-control-codes.md)。

 

