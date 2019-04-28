---
title: CD-ROM 独占访问模式
description: CD-ROM 独占访问模式
ms.assetid: 4432f6d6-e98c-4354-a7ba-b043a624f064
keywords:
- CD-ROM 驱动程序 WDK 存储
- 存储 CD-ROM 驱动程序 WDK
- 独占访问模式 WDK CD-ROM
- IOCTL_CDROM_EXCLUSIVE_ACCESS
- CDROM_EXCLUSIVE_LOCK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35a3afa58868488480354ec6dbf066bea51a14c1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338322"
---
# <a name="cd-rom-exclusive-access-mode"></a>CD-ROM 独占访问模式


在 CD-ROM*独占访问权*机制 (也称为*独占访问模式*) 使应用程序和系统组件，以获得独占访问权到 CD-ROM 设备。 需要对 CD-ROM 设备独占访问权限的应用程序包括以下示例：

<span id="Optical_media-authoring_applications"></span><span id="optical_media-authoring_applications"></span><span id="OPTICAL_MEDIA-AUTHORING_APPLICATIONS"></span>光学媒体创作应用程序  
某些光学创作软件需要独占访问权限给 CD-ROM 设备，以从其他应用程序写入数据，而不会造成任何中断。 否则，数据可能会编写不正确，从而导致数据损坏。

<span id="Firmware_update_utilities"></span><span id="firmware_update_utilities"></span><span id="FIRMWARE_UPDATE_UTILITIES"></span>固件更新实用程序  
许多 CD-ROM 设备制造商提供的固件更新实用程序。 如果应用程序发送命令到设备固件更新过程中，它可能会使该设备不可用。

而无需的独占访问机制，供应商为提供以下两种类型的应用程序独占访问权限的唯一方法是安装失败从其他应用程序和组件，I/O 请求的自定义筛选器驱动程序和此方法会导致系统不是稳定。 不应使用筛选器驱动程序来获得对 CD-ROM 设备的独占访问权限。

若要使用的独占访问机制，应用程序必须发送[ **IOCTL\_CDROM\_独占\_访问**](https://msdn.microsoft.com/library/windows/hardware/ff559327)在被动的 CD-ROM 类驱动程序的请求\_级别 IRQL。 当调用方发出此请求时，调用方必须提供中的标识字符串**CallerName**的成员[ **CDROM\_独占\_锁**](https://msdn.microsoft.com/library/windows/hardware/ff551363). 在类驱动程序使用此字符串来识别具有独占访问权限的应用程序。

应用程序应尝试将其锁定之前查询设备的当前状态。 如果设备已被锁定，在类驱动程序返回的当前所有者的设备的标识字符串。 在之前锁定设备，调用方必须打开它以读/写访问模式。 因此，调用方必须具有管理员权限或权限才能在写访问权限模式下打开 CD-ROM 设备。

因为保证 CD-ROM 类驱动程序将接收该请求，请求独占访问权限的调用方不应通过只需将创建请求发送到文件系统驱动程序，打开 CD-ROM 设备。 相反，应用程序应使用 **SetupDi * * * Xxx*例程枚举系统中的 CD-ROM 的所有设备的接口，然后打开相应的设备接口。

当调用方使用的驱动器号的打开设备或类似*CdRom0*保证文件系统驱动程序与设置为 0 的访问模式，将创建请求传递到 CD-ROM 类驱动程序。 但这种保证并仍足够，因为通过此过程来获取应用程序的句柄并未授予调用方读/写访问设备。

独占访问模式具有以下特征：

-   只有独占访问锁的所有者可以访问设备。

-   系统会从其他应用程序的访问请求失败。

-   系统进程和插即用 (PnP) 和 power I/O 请求数据包 (Irp) 以典型方式。

-   对设备禁用媒体更改通知。

-   系统未打开设备锁定时的请求。

-   发送的其他应用程序[ **IOCTL\_存储\_查询\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff560590)到 CD-ROM 类驱动程序的请求将收到来自缓存的信息设备锁定时。 具体而言，如果[**存储\_查询\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff566998)是**PropertyExistsQuery**，IOCTL 方式与其在设备时的行为相同未锁定。 此外，如果**存储\_查询\_类型**是**PropertyStandardQuery**并[**存储\_属性\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff566996)是**StorageDeviceProperty**或**StorageAdapterProperty**，IOCTL 返回 CD-ROM 类驱动程序中缓存的信息。 与其他的组合**存储\_查询\_类型**并**存储\_属性\_ID**，IOCTL 失败，出现状态值状态\_访问\_被拒绝。

-   发送的其他应用程序[ **IOCTL\_CDROM\_获取\_查询\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff559345) CD-ROM 类驱动程序的请求会收到缓存的信息从设备时它已锁定，且还时将其解锁。

当发生以下任一情况时，系统将删除到 CD-ROM 设备的独占访问权限：

-   独占访问锁的所有者发送[ **IOCTL\_CDROM\_独占\_访问**](https://msdn.microsoft.com/library/windows/hardware/ff559327) CD-ROM 类驱动程序通过对请求**RequestType**的成员[ **CDROM\_独占\_访问**](https://msdn.microsoft.com/library/windows/hardware/ff551362)设置为**ExclusiveAccessUnlockDevice**。

-   独占访问锁的所有者关闭设备句柄。

-   拥有独占访问权限锁定的应用程序终止。

删除设备上的独占访问权限锁定后, CD-ROM 类驱动程序将执行以下操作：

-   允许在设备上的介质更改通知。

-   设置执行\_验证\_卷标志在设备扩展中，因此，系统将重新安装设备的文件系统。

-   强制设备的多媒体功能的更新。

 

 




