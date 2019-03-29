---
title: 卷装载示例
description: 卷装载示例
ms.assetid: d6645d05-a945-4454-ac7c-122219bbdc50
keywords:
- 筛选器驱动程序 WDK 文件系统、 卷装入过程
- 文件系统筛选器驱动程序 WDK，卷装载进程
- 装载卷 WDK 的文件系统
- 卷 WDK 文件系统装载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2eee275923844f0def159692c13e85369457d7a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563194"
---
# <a name="volume-mount-example"></a>卷装载示例


## <span id="ddk_volume_mount_example_if"></span><span id="DDK_VOLUME_MOUNT_EXAMPLE_IF"></span>


下图显示了什么 CDFS 看起来像之前它已安装的任何卷。 在此示例中，两个筛选器已附加本身到 CDFS 控制设备对象。 （注意：包含 CDFS 控制设备对象的全局文件系统队列未显示。）

![说明卷装载之前 cdfs 的关系图](images/cdfsunmounted.png)

下图显示了一个典型的驱动程序堆栈，尚未载入为 CDFS 卷的 CD-ROM 存储设备。

![说明 cd-rom 之前卷装载的存储设备堆栈的关系图](images/cdromstack.png)

下图显示了文件系统驱动程序堆栈、 卷堆栈和 CD-ROM 存储设备堆栈外观后 CDFS 文件系统已装载到 CD-ROM 设备上的卷。

![说明已装载的 cdfs 卷的关系图](images/cdfsmountedstacks.png)

有关上图中的一些注意事项：

-   CDFS 控制设备对象窗体的文件系统驱动程序堆栈。 此堆栈的存储设备未装载，可以直接接收 Irp，也可以包含文件系统筛选器设备对象。 筛选器附加到文件系统控制设备对象，若要监视的卷装载 ([**IRP\_MJ\_文件\_系统\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff548670)，IRP\_MN\_装载\_卷) 的请求。 不需要命名为文件系统控制设备对象。 这使它们从文件系统卷设备对象，其永远不会为。

-   如图所示，尽管可以将第二个存储筛选器附加到 CD-ROM 存储设备堆栈的顶部，装入 CDFS 卷后，此筛选器将不会收到任何 Irp 传递的向下从文件系统堆栈到存储 d设备堆栈。 但是，它将接收任何 Irp，将直接发送到存储设备堆栈。

-   请务必注意，文件系统已装入卷后，存储设备堆栈仍可接收 Irp 直接。 具体而言，power Irp (IRP\_MJ\_POWER) 始终将直接发送到的存储设备堆栈，永远不会向文件系统堆栈。 (因此，例如，文件系统筛选器驱动程序应永远不会注册一个调度例程 IRP\_MJ\_中的 POWER 其**DriverEntry**例程。)

    但是，PnP Irp ([**IRP\_MJ\_PNP**](https://msdn.microsoft.com/library/windows/hardware/ff549268)) 可以发送到任一堆栈。 链接在文件系统卷上面的筛选器驱动程序应始终传递这些 Irp 到下一个较低的驱动程序默认情况下，以便文件系统卷设备可以传递到存储设备堆栈 Irp。

 

 




