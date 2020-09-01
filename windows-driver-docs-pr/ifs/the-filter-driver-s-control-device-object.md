---
title: 筛选器驱动程序的控制设备对象
description: 筛选器驱动程序的控制设备对象
ms.assetid: ac49b5d0-110d-4e47-814b-05f59791de41
keywords:
- 控制设备对象 WDK 文件系统
- CDOs WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a403e2ec4724409213538d06dc9ee9044a38fcdb
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067356"
---
# <a name="the-filter-drivers-control-device-object"></a>筛选器驱动程序的控制设备对象


## <span id="ddk_the_filter_drivers_control_device_object_if"></span><span id="DDK_THE_FILTER_DRIVERS_CONTROL_DEVICE_OBJECT_IF"></span>


与创建和使用命名控件设备对象 (CDO) 所需的文件系统不同，文件系统筛选器驱动程序不需要具有 CDO。 如果是这样，则可以选择性地命名此 CDO，表示系统的筛选器驱动程序。 其作用是接收来自用户模式应用程序的 i/o 请求， (或不太常见地) 其他内核模式驱动程序，并相应地对其进行操作。

大多数文件系统筛选器驱动程序创建和使用 CDO。 但是，在 CDO 上支持 i/o 请求是可选的。 若要提供此支持，筛选器驱动程序调用 [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice) 创建 CDO 时，必须提供对象的设备名称。 然后，用户模式应用程序可以通过调用 [**CreateFile**](/windows/desktop/api/fileapi/nf-fileapi-createfilea)获取已命名 CDO 的句柄，同时提供设备名称的用户模式版本。

例如，假设有一个假想的 "MyLegacyFilter" 内核模式驱动程序。 此驱动程序可以创建名称为的 CDO：

```cpp
\Device\MyLegacyFilter
```

并调用 [**IoCreateSymbolicLink**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesymboliclink) 将此名称链接到等效的用户模式可见名称。 这样做是为了使 MyLegacyFilter 的用户模式应用程序可以通过提供名称来打开内核模式驱动程序 CDO 的句柄：

```cpp
\\.\MyLegacyFilter
```

当它调用 [**CreateFile**](/windows/desktop/api/fileapi/nf-fileapi-createfilea)时。

### <a name="span-idtypes_of_i_o_requests_that_are_sent_to_the_filter_driver_s_control_devspanspan-idtypes_of_i_o_requests_that_are_sent_to_the_filter_driver_s_control_devspantypes-of-io-requests-that-are-sent-to-the-filter-drivers-control-device-object"></a><span id="types_of_i_o_requests_that_are_sent_to_the_filter_driver_s_control_dev"></span><span id="TYPES_OF_I_O_REQUESTS_THAT_ARE_SENT_TO_THE_FILTER_DRIVER_S_CONTROL_DEV"></span>发送到筛选器驱动程序的控制设备对象的 i/o 请求类型

文件系统筛选器驱动程序不需要支持控制设备对象上的任何 i/o 操作 (CDO) 。 但是，大多数筛选器都允许将以下类型的 i/o 请求发送到筛选器的 CDO：

-   [**IRP \_MJ " \_ 创建**](./irp-mj-create.md) (" 以打开目标设备对象的句柄，并为用户应用程序指定该句柄) 

-   [**IRP \_"MJ \_ 清除**](./irp-mj-cleanup.md) " (关闭目标设备对象的用户模式应用程序的句柄) 

-   [**IRP \_MJ \_ close**](./irp-mj-close.md) (关闭目标设备对象的上一个剩余打开句柄) 

-   [**IRP \_MJ \_ 设备 \_ 控制**](./irp-mj-device-control.md)、 [**IRP \_ MJ \_ 文件 \_ 系统 \_ 控制**](./irp-mj-file-system-control.md)或 **FastIoDeviceControl** (向筛选器驱动程序发送专用 IOCTLs 或 FSCTLs) 

请注意，与文件系统筛选器驱动程序创建的所有其他设备对象不同，CDO 不会附加到驱动程序堆栈。 未在筛选器驱动程序的 CDO 上方或下方附加任何设备对象。 因此，对于收到的任何 i/o 请求，CDO 都可以安全地假定它是唯一的目标接收者。 对于筛选器设备对象或文件系统 CDOs，这种情况并不适用。 相应地，CDO 必须最终完成它收到的每个 IRP。 对于快速 i/o 请求，它必须返回 **TRUE** 或 **FALSE**。

 

