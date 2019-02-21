---
title: 筛选器驱动程序的控制设备对象
description: 筛选器驱动程序的控制设备对象
ms.assetid: ac49b5d0-110d-4e47-814b-05f59791de41
keywords:
- 控制设备对象 WDK 文件系统
- CDOs WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f93fe614dc97a10f571e7eb443415312c190135e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555023"
---
# <a name="the-filter-drivers-control-device-object"></a>筛选器驱动程序的控制设备对象


## <span id="ddk_the_filter_drivers_control_device_object_if"></span><span id="DDK_THE_FILTER_DRIVERS_CONTROL_DEVICE_OBJECT_IF"></span>


与文件系统，需要创建和使用已命名的控制设备对象 (CDO)，不同的文件系统筛选器驱动程序不需要具有 CDO。 如果是这样，此 CDO，可以根据需要命名，表示系统筛选器驱动程序。 其作用是从用户模式应用程序接收的 I/O 请求 (或不太常见的是，另一个内核模式驱动程序)，并相应地对其采取措施。

大多数文件系统筛选器驱动程序创建并使用 CDO。 但是，对 CDO 上的 I/O 请求的支持是可选的。 提供此支持，当筛选器驱动程序调用[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)若要创建 CDO，它必须提供该对象的设备名称。 用户模式应用程序然后可以通过调用获取的句柄命名 CDO [ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)，提供设备名称的用户模式版本。

例如，考虑假设"MyLegacyFilter"内核模式驱动程序。 此驱动程序可以使用该名称创建 CDO:

```cpp
\Device\MyLegacyFilter
```

并调用[ **IoCreateSymbolicLink** ](https://msdn.microsoft.com/library/windows/hardware/ff549043)若要将此名称链接到一个用户模式下可见的等效名称。 这是以便 MyLegacyFilter 的用户模式应用程序可以打开的句柄内核模式驱动程序的 CDO 提供名称：

```cpp
\\.\MyLegacyFilter
```

当调用[ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)。

### <a name="span-idtypesofiorequeststhataresenttothefilterdriverscontroldevspanspan-idtypesofiorequeststhataresenttothefilterdriverscontroldevspantypes-of-io-requests-that-are-sent-to-the-filter-drivers-control-device-object"></a><span id="types_of_i_o_requests_that_are_sent_to_the_filter_driver_s_control_dev"></span><span id="TYPES_OF_I_O_REQUESTS_THAT_ARE_SENT_TO_THE_FILTER_DRIVER_S_CONTROL_DEV"></span>类型的 I/O 请求发送到筛选器驱动程序的控制设备对象

文件系统筛选器驱动程序不支持所需的控制设备对象 (CDO) 上的任何 I/O 操作。 但是，大多数筛选器允许以下类型的 I/O 请求发送到筛选器的 CDO:

-   [**IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff548630) （若要打开的句柄的目标设备对象，并为该句柄提供对用户应用程序）

-   [**IRP\_MJ\_清理**](https://msdn.microsoft.com/library/windows/hardware/ff548608) （若要关闭到目标设备对象的用户模式应用程序的句柄）

-   [**IRP\_MJ\_关闭**](https://msdn.microsoft.com/library/windows/hardware/ff548621) （若要关闭的最后一个剩余打开句柄的目标设备对象）

-   [**IRP\_MJ\_设备\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff548649)， [ **IRP\_MJ\_文件\_系统\_控件** ](https://msdn.microsoft.com/library/windows/hardware/ff548670)，或**FastIoDeviceControl** （若要将专用 Ioctl 或 FSCTLs 发送到筛选器驱动程序）

请注意，与所有其他设备创建的对象的文件系统筛选器驱动程序，不同 CDO 未附加到驱动程序堆栈。 高于或低于筛选器驱动程序的 CDO 不附加任何设备对象。 因此，对于接收任何 I/O 请求，CDO 可以安全地假定它是唯一的目标接收方。 这不是筛选设备对象或文件系统 CDOs，则返回 true。 相应地，CDO 最终必须完成接收每个 IRP。 对于快速 I/O 请求，它必须返回 **，则返回 TRUE**或**FALSE**。

 

 




