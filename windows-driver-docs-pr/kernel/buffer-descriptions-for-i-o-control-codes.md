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
ms.openlocfilehash: 084a6c5a801b94112c6891f1948cb880ef9cf381
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837172"
---
# <a name="buffer-descriptions-for-io-control-codes"></a>I/O 控制代码的缓冲区说明





I/o 控制代码包含在[**IRP\_mj\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)和[**IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)请求。 由于对[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)的调用（如 Microsoft Windows SDK 文档中所述）和[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)，i/o 管理器将创建这些请求。

由于[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)和**IoBuildDeviceIoControlRequest**同时接受输入缓冲区和输出缓冲区作为参数，因此所有**IRP 都\_mj\_设备\_控制**和**IRP\_MJ\_内部\_设备\_控制**请求同时提供输入缓冲区和输出缓冲区。 系统描述这些缓冲区的方式取决于数据传输类型。 传输类型由用于创建 IOCTL 代码值的[**CTL\_代码**](defining-i-o-control-codes.md)宏中的*TransferType*值指定。

系统说明每个*TransferType*值的缓冲区，如下所示：

<a href="" id="method-buffered"></a>\_缓冲的方法  
对于此传输类型，Irp 提供一个指向**Irp&gt;SystemBuffer**的缓冲区的指针。 此缓冲区表示在对[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)和**IoBuildDeviceIoControlRequest**的调用中指定的输入缓冲区和输出缓冲区。 该驱动程序会将数据传入或传出此缓冲区。

对于输入数据，缓冲区大小由驱动程序的[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构中的**DeviceIoControl。** 对于输出数据，缓冲区大小由驱动程序的**IO\_堆栈\_位置**结构中的**DeviceIoControl。**

系统为单个输入/输出缓冲区分配的空间大小是两个长度值中较大的一个。

<a href="" id="method-in-direct-or-method-out-direct"></a>方法\_\_直接或方法\_OUT\_直接  
对于这些传输类型，Irp 提供指向**Irp&gt;SystemBuffer**的缓冲区的指针。 这表示对**DeviceIoControl**和**IoBuildDeviceIoControlRequest**的调用中指定的输入缓冲区。 缓冲区大小由驱动程序的**IO\_堆栈\_位置**结构中的**DeviceIoControl。**

对于这些传输类型，Irp 还向 Irp 提供一个指向 MDL **&gt;MdlAddress**的指针。 这表示对[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)和**IoBuildDeviceIoControlRequest**的调用中指定的输出缓冲区。 但是，此缓冲区实际可用作输入缓冲区或输出缓冲区，如下所示：

-   如果处理 IRP 的驱动程序在调用时接收到缓冲区中的数据，则指定\_DIRECT\_方法。 MDL 描述了输入缓冲区，并在\_DIRECT 中指定方法\_可确保执行线程具有对缓冲区的读取访问权限。

-   如果处理 IRP 的驱动程序在完成 IRP 之前将数据写入缓冲区，则指定方法\_OUT\_DIRECT。 MDL 描述了输出缓冲区，并指定方法\_OUT\_直接确保执行线程对缓冲区具有写入访问权限。

对于这两种传输类型， **DeviceIoControl. OutputBufferLength**指定 MDL 描述的缓冲区大小。

<a href="" id="method-neither"></a>方法\_均不  
I/o 管理器不提供任何系统缓冲区或 MDLs。 IRP 提供指定给**DeviceIoControl**或**IoBuildDeviceIoControlRequest**的输入和输出缓冲区的用户模式虚拟地址，而无需对其进行验证或映射。

输入缓冲区的地址由驱动程序的**IO\_堆栈\_位置**结构中的**DeviceIoControl. Type3InputBuffer**提供，输出缓冲区的地址由**Irp-&gt;UserBuffer**指定。

缓冲区大小由驱动程序的**IO\_堆栈\_位置**结构中的**InputBufferLength**和**DeviceIoControl**提供。

有关**CTL\_代码**宏以及上面列出的传输类型的详细信息，请参阅[定义 i/o 控制代码](defining-i-o-control-codes.md)。

 

 




