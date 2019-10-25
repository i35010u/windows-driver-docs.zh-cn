---
title: CD-ROM 独占访问模式
description: CD-ROM 独占访问模式
ms.assetid: 4432f6d6-e98c-4354-a7ba-b043a624f064
keywords:
- CD-ROM 驱动程序 WDK 存储
- 存储 cd-rom 驱动程序 WDK
- 独占访问模式 WDK cd-rom
- IOCTL_CDROM_EXCLUSIVE_ACCESS
- CDROM_EXCLUSIVE_LOCK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 481511f34a27c5fd4e72bd5b7c65aea4b2ea453b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841635"
---
# <a name="cd-rom-exclusive-access-mode"></a>CD-ROM 独占访问模式


Cd-rom*独占访问*机制（也称为*独占访问模式*）使应用程序和系统组件能够获取对 cd-rom 设备的独占访问权限。 需要对 CD-ROM 设备进行独占访问的应用程序包括以下示例：

<span id="Optical_media-authoring_applications"></span><span id="optical_media-authoring_applications"></span><span id="OPTICAL_MEDIA-AUTHORING_APPLICATIONS"></span>光学媒体-创作应用程序  
某些光学创作软件需要独占访问 CD-ROM 设备才能写入数据，而不会中断其他应用程序。 否则，可能会错误地写入数据，从而导致数据损坏。

<span id="Firmware_update_utilities"></span><span id="firmware_update_utilities"></span><span id="FIRMWARE_UPDATE_UTILITIES"></span>固件更新实用工具  
Cd-rom 设备的许多制造商提供固件更新实用程序。 如果应用程序在固件更新过程中将命令发送到设备，则可能会使该设备不可用。

如果没有独占访问机制，供应商提供这两种类型的应用程序的唯一方式是安装自定义筛选器驱动程序，该驱动程序将无法从其他应用程序和组件进行 i/o 请求，这种方法会导致系统稳定性. 不应使用筛选器驱动程序来获取对 cd-rom 设备的独占访问权限。

若要使用独占访问机制，应用程序必须将[**IOCTL\_CDROM\_独占\_访问**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_exclusive_access)请求发送到被动\_级别 IRQL 的 cd-rom 类驱动程序。 调用方发出此请求时，调用方必须提供 CDROM 的**CallerName**成员中的标识字符串[ **\_独占\_锁**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ns-ntddcdrm-_cdrom_exclusive_lock)。 类驱动程序使用此字符串来标识具有独占访问权限的应用程序。

应用程序在尝试锁定设备之前应查询设备的当前状态。 如果设备已锁定，类驱动程序将返回当前设备所有者的标识字符串。 在锁定设备之前，调用方必须以读/写访问模式打开它。 因此，调用方必须具有管理员权限或在写访问模式下打开 cd-rom 设备的权限。

请求独占访问的调用方不应通过只将创建请求发送到文件系统驱动程序来打开 CD-ROM 设备，因为无法保证 cd-rom 类驱动程序将接收该请求。 相反，应用程序应使用**SetupDi**_Xxx_例程来枚举系统中所有 cd-rom 设备的接口，然后打开相应的设备接口。

当调用方使用驱动器号或名称（如*CdRom0* ）打开设备时，如果访问模式设置为0，则系统驱动程序将保证将创建请求传递到 cd-rom 类驱动程序。 但这一保证仍不足，因为此过程获取的句柄不会向调用方授予对设备的读/写访问权限。

独占访问模式具有以下特征：

-   只有独占访问锁定的所有者才能访问设备。

-   系统将无法从其他应用程序访问请求。

-   系统以典型方式处理即插即用（PnP）和电源 i/o 请求数据包（Irp）。

-   已禁用设备的媒体更改通知。

-   当设备处于锁定状态时，系统将无法打开该设备的请求。

-   将[**IOCTL\_存储\_QUERY\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)请求发送到 cd-rom 类驱动程序的其他应用程序将会在设备锁定时接收缓存的信息。 具体来说，如果[**存储\_查询\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ne-ntddstor-_storage_query_type)为**PROPERTYEXISTSQUERY**，则 IOCTL 的行为与设备未锁定时的行为相同。 此外，如果**存储\_查询\_类型**为**PropertyStandardQuery** ，并且[**存储\_属性\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ne-ntddstor-storage_property_id)是**StorageDeviceProperty**或**StorageAdapterProperty**，则 IOCTL 返回cd-rom 类驱动程序中缓存的信息。 使用**存储\_查询**的其他组合\_类型和**存储\_属性\_ID**，IOCTL 失败，状态值状态\_访问\_被拒绝。

-   发送[**IOCTL\_CDROM\_的其他应用程序获取\_查询\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_inquiry_data)向 cd-rom 类驱动程序发送缓存信息时，从设备中接收缓存的信息以及解锁。

当出现下列任一情况时，系统会删除对 CD-ROM 设备的独占访问权限：

-   独占访问锁定的所有者将[**IOCTL\_cdrom\_独占\_访问**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_exclusive_access)请求与 CDROM 的**RequestType**成员一起发送到 cd-rom 类驱动程序， [ **\_独占\_访问权限**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ns-ntddcdrm-_cdrom_exclusive_access)设置为**ExclusiveAccessUnlockDevice**。

-   独占访问锁定的所有者将关闭设备句柄。

-   拥有独占访问锁定的应用程序将终止。

删除设备上的独占访问锁定后，cd-rom 类驱动程序会执行以下操作：

-   启用设备上的媒体更改通知。

-   在设备扩展中设置 DO\_验证\_VOLUME 标志，使系统能够重新装载设备的文件系统。

-   强制更新设备的多媒体功能。

 

 




