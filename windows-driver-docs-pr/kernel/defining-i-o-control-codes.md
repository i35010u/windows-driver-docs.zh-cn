---
title: 定义 I/O 控制代码
description: 定义 I/O 控制代码
ms.assetid: 967b0199-e9a0-4c8d-9130-c81436c59ca3
keywords:
- I/O 控制代码 WDK 内核，定义
- 控制代码 WDK Ioctl，定义
- Ioctl WDK 内核，定义
- CTL_CODE 宏
- Ioctl WDK 用户模式
- 用户模式组件 WDK Ioctl
- I/O 控制代码 WDK 用户模式
- 控制代码 WDK 用户模式
- 布局 WDK Ioctl
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d7a39ed0d7b80cef7896f75d27f7b206cad137c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545322"
---
# <a name="defining-io-control-codes"></a>定义 I/O 控制代码





定义新 Ioctl，时，请务必记住以下规则：

-   如果新 IOCTL 将可供用户模式下的软件组件，必须与使用 IOCTL [ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744)请求。 用户模式组件发送**IRP\_MJ\_设备\_控制**请求通过调用[ **DeviceIoControl**](https://msdn.microsoft.com/library/windows/desktop/aa363216)，这是Win32 函数。
-   如果新 IOCTL 将仅适用于内核模式驱动程序组件，必须与使用 IOCTL [ **IRP\_MJ\_内部\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550766)请求。 内核模式组件创建**IRP\_MJ\_内部\_设备\_控制**通过调用请求**IoBuildDeviceIoControlRequest**。 有关详细信息，请参阅[驱动程序中创建 IOCTL 请求](creating-ioctl-requests-in-drivers.md)。

I/O 控制代码是一个 32 位值的多个字段组成。 下图说明了 I/O 控制代码的布局。

![说明的 i/o 控制代码布局的关系图](images/ioctl-1.png)

使用系统提供**CTL\_代码**wdm.h 中和 Ntddk.h，可以定义新的 I/O 控制代码中定义的宏。 新 IOCTL 定义代码，不管是适用于**IRP\_MJ\_设备\_控制**或**IRP\_MJ\_内部\_设备\_控制**请求时，使用以下格式：

```cpp
#define IOCTL_Device_Function CTL_CODE(DeviceType, Function, Method, Access)
```

选择的 IOCTL，窗体 IOCTL 的说明性常量名称\_*设备*\_*函数*，其中*设备*指示的类型设备和*函数*指示的操作。 示例常量名称是 IOCTL\_视频\_启用\_游标。

将以下参数传递给**CTL\_代码**宏：

<a href="" id="devicetype"></a>*DeviceType*  
标识设备类型。 此值必须匹配在中设置的值**DeviceType**驱动程序的成员[**设备\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff543147)结构。 (请参阅[指定设备类型](specifying-device-types.md))。 值小于 0x8000 仅供 Microsoft。 可以由供应商使用 0x8000 和更高版本的值。 请注意，设置供应商分配值**常见**位。

<a href="" id="functioncode"></a>*FunctionCode*  
标识要由驱动程序执行的函数。 值小于 0x800 仅供 Microsoft。 可以由供应商使用 0x800 和更高版本的值。 请注意，设置供应商分配值**自定义**位。

<a href="" id="transfertype"></a>*TransferType*  
指示系统之间的调用方传递数据时如何[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216) (或[ **IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)) 和处理 IRP 驱动程序。

使用系统定义的以下常量之一：

<a href="" id="method-buffered"></a>方法\_缓冲  
指定[缓冲 I/O](methods-for-accessing-data-buffers.md)方法，它通常用于传输较少的每个请求的数据。 大多数设备和中间驱动程序的 I/O 控制代码使用此*留空，则*值。

有关如何在系统的方法指定数据缓冲区\_缓冲 I/O 控制代码，请参阅[I/O 控制代码的缓冲区说明](buffer-descriptions-for-i-o-control-codes.md)。

有关缓冲 I/O 的详细信息，请参阅[使用缓冲 I/O](using-buffered-i-o.md)。

<a href="" id="method-in-direct-or-method-out-direct"></a>方法\_IN\_直接访问或通过方法\_出\_直接  
指定[直接 I/O](methods-for-accessing-data-buffers.md)方法，它通常用于读取或写入大量数据，使用 DMA 或 PIO，必须快速传输。

指定方法\_IN\_直接 if 的调用方[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)或者**IoBuildDeviceIoControlRequest**会将数据传递到驱动程序。

指定方法\_出\_直接如果的调用方[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)或者**IoBuildDeviceIoControlRequest**将接收中的数据驱动程序。

有关如何在系统的方法指定数据缓冲区\_IN\_DIRECT 和方法\_OUT\_直接 I/O 控制代码，请参阅[的 I/O 控制代码缓冲区说明](buffer-descriptions-for-i-o-control-codes.md).

有关直接 I/O 的详细信息，请参阅[使用直接 I/O](using-direct-i-o.md)。

<a href="" id="method-neither"></a>方法\_NEITHER  
指定[既不缓冲，也不直接 I/O](using-neither-buffered-nor-direct-i-o.md)。 I/O 管理器不提供任何系统缓冲区或 MDLs。 IRP 提供到指定的输入和输出缓冲区的用户模式虚拟地址[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)或**IoBuildDeviceIoControlRequest**，而无需验证或将其映射。

有关如何在系统的方法指定数据缓冲区\_既不 I/O 控制代码，请参阅[I/O 控制代码的缓冲区说明](buffer-descriptions-for-i-o-control-codes.md)。

可以使用此方法，仅当该驱动程序可以保证以发起 I/O 控制请求的线程的上下文中运行。 仅最高级别的内核模式驱动程序保证满足此条件，因此方法\_既不很少使用的传递给低级别的设备驱动程序的 I/O 控制代码。

使用此方法，最高级别的驱动程序必须确定是否设置缓冲或直接访问用户数据在收到请求时，可能必须锁定用户缓冲区，并必须在结构化的异常处理程序中包装对用户缓冲区的访问权限 (请参阅<c1/1>处理的异常](handling-exceptions.md))。 否则，原始用户模式下调用方可能会更改缓冲的数据之前，驱动程序可以使用它，或调用方无法换出，就像该驱动程序正在访问的用户缓冲区。

有关详细信息，请参阅[使用既不缓冲 Nor 直接 I/O](using-neither-buffered-nor-direct-i-o.md)。

<a href="" id="requiredaccess"></a>*RequiredAccess*  
指示调用方必须请求的访问类型打开文件对象，表示设备时 (请参阅[ **IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff550729))。 I/O 管理器将创建 Irp，并调用驱动程序和特定的 I/O 控制代码，仅当调用方已请求指定的访问权限。 *RequiredAccess*指定通过使用系统定义的以下常量：

<a href="" id="file-any-access"></a>文件\_ANY\_访问  
I/O 管理器将 IRP 发送的任何调用方具有的句柄表示的目标设备对象的文件对象。

<a href="" id="file-read-data"></a>FILE\_READ\_DATA  
I/O 管理器将 IRP 发送仅对调用方使用读取访问权限，允许基础设备驱动程序将数据从设备传输到系统内存。

<a href="" id="file-write-data"></a>FILE\_WRITE\_DATA  
I/O 管理器将 IRP 发送仅对调用方的写访问权限，允许基础设备驱动程序将从系统内存的数据传输到其设备。

文件\_读\_数据和文件\_编写\_数据可以一起地是或运算，如果调用方必须具有读取和写入访问权限。

一些系统定义的 I/O 控制代码已*RequiredAccess*文件的值\_ANY\_访问权限，允许调用者发送到设备的特定 IOCTL 而不考虑授予的访问权限。 示例包括发送到的驱动程序的 I/O 控制代码*独占设备*。

其他系统定义的 I/O 控制代码需要调用方拥有读取访问权限、 写访问权限，或两者。 例如，以下定义的公共的 I/O 控制代码 IOCTL\_磁盘\_设置\_分区\_信息显示，此 I/O 请求可以发送到驱动程序仅当调用方具有的读和写访问权限权限：

```cpp
#define IOCTL_DISK_SET_PARTITION_INFO\
        CTL_CODE(IOCTL_DISK_BASE, 0x008, METHOD_BUFFERED,\
        FILE_READ_DATA | FILE_WRITE_DATA)
```

**请注意**  之前指定文件\_ANY\_访问对于新 IOCTL 代码，您必须是完全确定允许不受限制的访问你的设备不会创建到的恶意用户可能的路径危害系统。

 

驱动程序可以使用[ **IoValidateDeviceIoControlAccess** ](https://msdn.microsoft.com/library/windows/hardware/ff550418)执行更严格的访问检查所提供的 IOCTL 相比*RequiredAccess*位。

## <a name="other-useful-macros"></a>其他有用的宏


下列宏可用于提取 16 位*DeviceType*和 2 位*留空，则*IOCTL 代码中的字段：

```cpp
#define DEVICE_TYPE_FROM_CTL_CODE(ctrlCode)   (((ULONG)(ctrlCode & 0xffff0000)) >> 16)
#define METHOD_FROM_CTL_CODE(ctrlCode)        ((ULONG)(ctrlCode & 3))
```

这些宏 wdm.h 中和 Ntddk.h 中定义。

 

 




