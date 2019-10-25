---
title: 装载卷
description: 装载卷
ms.assetid: 0531b023-f35c-4fe9-9c0d-5acafc42f9b4
keywords:
- 筛选器驱动程序 WDK 文件系统，卷装入过程
- 文件系统筛选器驱动程序 WDK，卷装入过程
- 卷 WDK 文件系统，装载
- 装载卷 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f38e0dddcc2cffeac40a0d3a9615253cb7e1860
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841119"
---
# <a name="mounting-a-volume"></a>装载卷


## <span id="ddk_mounting_a_volume_if"></span><span id="DDK_MOUNTING_A_VOLUME_IF"></span>


卷装入过程通常由在逻辑卷（即分区或动态卷）上打开文件的请求触发，如下所示：

1.  用户应用程序调用**CreateFile**来打开文件。 或内核模式驱动程序调用[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)或[**IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)。

2.  I/o 管理器确定请求的目标是哪个逻辑卷，并检查其设备对象以查看它是否已装入。 如果设置了 VPB\_装入的标志，则文件系统已装载卷。

3.  如果自系统启动以来文件系统尚未装载该卷（即，未设置 VPB\_装载标志），则 i/o 管理器会将卷装入（[**IRP\_MJ\_文件\_系统\_控制**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)，IRP\_MN\_将\_卷）请求装入每个可能声称卷的文件系统。

    并非所有内置文件系统都一定会在系统启动后加载。 （请参阅[系统启动过程中对文件系统的影响](what-happens-to-file-systems-during-system-boot.md)。）对于尚未加载的内置文件系统，i/o 管理器会将卷装入请求发送到文件系统识别器（FsRec），这会代表这些文件系统检查卷引导扇区。

    如果 FsRec 确定卷是由尚未加载的文件系统格式化的，则 i/o 管理器通过发送加载文件系统（[**irp\_MJ\_文件\_系统\_控制**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)、IRP\_MN\_LOAD\_文件来做出响应\_系统）对 FsRec 的请求，该请求加载文件系统。 然后，i/o 管理器将原始的卷装入请求发送到文件系统。

4.  每个接收装载卷请求的文件系统将检查卷的启动扇区，以确定卷的格式和其他信息是否指示该卷已由该特定文件系统格式化。 如果格式匹配，则文件系统会装载卷。

以下各节讨论文件系统在识别后如何装载卷：

[卷的装载方式](how-the-volume-is-mounted.md)

[卷装入示例](volume-mount-example.md)

 

 




