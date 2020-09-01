---
title: 定义 I/O 控制代码
description: 定义 I/O 控制代码
ms.assetid: 967b0199-e9a0-4c8d-9130-c81436c59ca3
keywords:
- I/o 控制代码 WDK 内核，定义
- 控制代码 WDK IOCTLs，定义
- IOCTLs WDK 内核，定义
- CTL_CODE 宏
- IOCTLs WDK 用户模式
- 用户模式组件 WDK IOCTLs
- I/o 控制代码 WDK 用户模式
- 控制代码 WDK 用户模式
- 布局 WDK IOCTLs
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: db92cd1849f08558cbc44335056ea6be06c83485
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189819"
---
# <a name="defining-io-control-codes"></a>定义 I/O 控制代码





定义新的 IOCTLs 时，请务必记住以下规则：

-   如果新 IOCTL 将可用于用户模式软件组件，则 IOCTL 必须与 [**IRP \_ MJ \_ 设备 \_ 控制**](./irp-mj-device-control.md) 请求一起使用。 用户模式组件通过调用[**DeviceIoControl**](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)（Win32 函数）发送**IRP \_ MJ \_ 设备 \_ 控制**请求。
-   如果新 IOCTL 仅适用于内核模式驱动程序组件，则 IOCTL 必须与 [**IRP \_ MJ \_ 内部 \_ 设备 \_ 控制**](./irp-mj-internal-device-control.md) 请求一起使用。 内核模式组件通过调用**IoBuildDeviceIoControlRequest**创建**IRP \_ MJ \_ 内部 \_ 设备 \_ 控制**请求。 有关详细信息，请参阅 [在驱动程序中创建 IOCTL 请求](creating-ioctl-requests-in-drivers.md)。

I/o 控制代码是由多个字段组成的32位值。 下图说明了 i/o 控制代码的布局。

![说明 i/o 控制代码布局的关系图](images/ioctl-1.png)

使用在 Wdm .h 和 Ntddk 中定义的系统提供的 **CTL \_ 代码** 宏定义新的 i/o 控制代码。 定义新的 IOCTL 代码（无论是用于 **IRP \_ mj \_ 设备 \_ 控制** 还是 **irp \_ mj \_ 内部 \_ 设备 \_ 控制** 请求），都使用以下格式：

```cpp
#define IOCTL_Device_Function CTL_CODE(DeviceType, Function, Method, Access)
```

为 ioctl 选择一个描述性常量名称，其形式为 ioctl \_ *设备* \_ *函数*，其中*设备*指示设备的类型和*函数*指示操作。 示例常量名称为 IOCTL \_ 视频 \_ ENABLE \_ CURSOR。

向 **CTL \_ 代码** 宏提供以下参数：

<a href="" id="devicetype"></a>*DeviceType*  
标识设备类型。 此值必须与驱动程序的[**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构的**DeviceType**成员中设置的值匹配。  (参阅) [指定设备类型](specifying-device-types.md) 。 为 Microsoft 保留小于0x8000 的值。 供应商可以使用0x8000 和更高的值。 请注意，供应商分配的值设置了 **公共** 位。

<a href="" id="functioncode"></a>*FunctionCode*  
标识要由驱动程序执行的函数。 为 Microsoft 保留小于0x800 的值。 供应商可以使用0x800 和更高的值。 请注意，供应商分配的值设置 **自定义** 位。

<a href="" id="transfertype"></a>*TransferType*  
指示系统如何在 [**DeviceIoControl**](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) (或 [**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)) 的调用方与处理 IRP 的驱动程序之间传递数据。

使用以下系统定义的常量之一：

<a href="" id="method-buffered"></a>方法 \_ 缓冲  
指定 [缓冲 i/o](methods-for-accessing-data-buffers.md) 方法，该方法通常用于传输每个请求的少量数据。 设备和中间驱动程序的大多数 i/o 控制代码都使用此 *TransferType* 值。

有关系统如何为方法缓冲 i/o 控制代码指定数据缓冲区的信息 \_ ，请参阅 [I/o 控制代码的缓冲区说明](buffer-descriptions-for-i-o-control-codes.md)。

有关缓冲 i/o 的详细信息，请参阅 [使用缓冲 i/o](using-buffered-i-o.md)。

<a href="" id="method-in-direct-or-method-out-direct"></a>\_ \_ 直接或方法 \_ OUT \_ 直接的方法  
指定 [直接 i/o](methods-for-accessing-data-buffers.md) 方法，该方法通常用于读取或写入大量数据，使用 DMA 或 PIO 时必须快速传输。

\_ \_ 如果[**DeviceIoControl**](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)或**IoBuildDeviceIoControlRequest**的调用方将数据传递给驱动程序，请直接指定方法。

\_ \_ 如果[**DeviceIoControl**](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)或**IoBuildDeviceIoControlRequest**的调用方将接收来自驱动程序的数据，请指定 OUT 直接方法。

有关系统如何为直接 i/o 控制代码中的方法指定数据缓冲区的信息 \_ \_ \_ \_ ，请参阅 [I/o 控制代码的缓冲区说明](buffer-descriptions-for-i-o-control-codes.md)。

有关直接 i/o 的详细信息，请参阅 [使用直接 i/o](using-direct-i-o.md)。

<a href="" id="method-neither"></a>方法 \_ 都不是  
[不指定缓冲的和直接](using-neither-buffered-nor-direct-i-o.md)i/o。 I/o 管理器不提供任何系统缓冲区或 MDLs。 IRP 提供指定给 [**DeviceIoControl**](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) 或 **IoBuildDeviceIoControlRequest**的输入和输出缓冲区的用户模式虚拟地址，而无需对其进行验证或映射。

有关系统如何为方法的 i/o 控制代码指定数据缓冲区的信息 \_ ，请参阅 [I/o 控制代码的缓冲区说明](buffer-descriptions-for-i-o-control-codes.md)。

仅当驱动程序可以保证在发起 i/o 控制请求的线程的上下文中运行时，才可以使用此方法。 仅保证最高级别的内核模式驱动程序能够满足此条件，因此，此方法不 \_ 很少用于传递到低级别设备驱动程序的 i/o 控制代码。

使用此方法时，最高级别的驱动程序必须确定是否在收到请求时设置缓冲或直接访问用户数据，可能必须锁定用户缓冲区，并且必须在结构化异常处理程序中包装其对用户缓冲区的访问 (参阅 [处理异常](handling-exceptions.md)) 。 否则，原始用户模式调用方可能会在驱动程序可以使用缓冲的数据之前更改它们，也可以像驱动程序访问用户缓冲区那样换出调用方。

有关详细信息，请参阅 [不使用缓冲和直接 i/o](using-neither-buffered-nor-direct-i-o.md)。

<a href="" id="requiredaccess"></a>*RequiredAccess*  
指示调用方在打开表示设备 (的文件对象时必须请求的访问类型，请参阅 [**IRP \_ MJ \_ CREATE**](./irp-mj-create.md)) 。 仅当调用方请求指定的访问权限时，i/o 管理器才会创建 Irp 并使用特定 i/o 控制代码调用该驱动程序。 *RequiredAccess* 是使用以下系统定义的常量指定的：

<a href="" id="file-any-access"></a>文件 \_ 任何 \_ 访问权限  
I/o 管理器将为具有表示目标设备对象的文件对象的句柄的任何调用方发送 IRP。

<a href="" id="file-read-data"></a>文件 \_ 读取 \_ 数据  
I/o 管理器仅为具有读取访问权限的调用方发送 IRP，允许基础设备驱动程序将数据从设备传输到系统内存。

<a href="" id="file-write-data"></a>文件 \_ 写入 \_ 数据  
I/o 管理器只为具有写访问权限的调用方发送 IRP，这允许基础设备驱动程序将数据从系统内存传输到其设备。

\_ \_ \_ \_ 如果调用方必须同时具有读取和写入访问权限，则可以将文件读取数据和文件写入数据运算在一起。

某些系统定义的 i/o 控制代码的 *RequiredAccess* 值为 FILE \_ ANY \_ access，这允许调用方发送特定 IOCTL，而不考虑授予该设备的访问权限。 示例包括发送到 *独占设备*驱动程序的 i/o 控制代码。

其他系统定义的 i/o 控制代码要求调用方具有读取访问权限和/或写入访问权限。 例如，以下对公共 i/o 控制代码 IOCTL \_ 磁盘 \_ 集 \_ 分区信息的定义 \_ 显示：只有当调用方同时具有读取和写入访问权限时，才能将此 i/o 请求发送到驱动程序：

```cpp
#define IOCTL_DISK_SET_PARTITION_INFO\
        CTL_CODE(IOCTL_DISK_BASE, 0x008, METHOD_BUFFERED,\
        FILE_READ_DATA | FILE_WRITE_DATA)
```

**注意**   \_ \_ 为新的 IOCTL 代码指定 FILE ANY access 之前，必须完全确定允许对设备进行不受限制的访问不会为恶意用户创建可能的路径来损害系统。

 

驱动程序可以使用 [**IoValidateDeviceIoControlAccess**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iovalidatedeviceiocontrolaccess) 来执行更严格的访问检查，而不是由 IOCTL 的 *RequiredAccess* 位提供的。

## <a name="other-useful-macros"></a>其他有用的宏


以下宏适用于从 IOCTL 代码中提取16位 *DeviceType* 和2位 *TransferType* 字段：

```cpp
#define DEVICE_TYPE_FROM_CTL_CODE(ctrlCode)   (((ULONG)(ctrlCode & 0xffff0000)) >> 16)
#define METHOD_FROM_CTL_CODE(ctrlCode)        ((ULONG)(ctrlCode & 3))
```

这些宏在 Ntddk 和中定义。

 

