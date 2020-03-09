---
title: 如何识别卷
description: 如何识别卷
ms.assetid: 0531b023-f35c-4fe9-9c0d-5acafc42f9b4
keywords:
- 筛选器驱动程序，WDK 文件系统，卷装入进程，识别卷
- 文件系统筛选器驱动程序 WDK，卷装入进程，识别卷
- 卷 WDK 文件系统，装载
- 装载卷 WDK 文件系统
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5c70a05f7d9e8cacae2ef4fece6d45a6b830a6a3
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910526"
---
# <a name="how-the-volume-is-recognized"></a>如何识别卷

> [!NOTE]
> 为了获得最佳的可靠性和性能，请使用带有筛选器管理器支持的[文件系统微筛选器驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-concepts)，而不是使用旧的文件系统 若要将旧驱动程序移植到微筛选器驱动程序，请参阅[迁移旧筛选器驱动程序的准则](guidelines-for-porting-legacy-filter-drivers.md)。

卷装入过程通常由在逻辑卷（即分区或动态卷）上打开文件的请求触发，如下所示：

1. 用户应用程序调用**CreateFile**来打开文件。 或内核模式驱动程序调用[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)或[**IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)。

2. I/o 管理器确定请求的目标是哪个逻辑卷，并检查其设备对象以查看它是否已装入。 如果设置了 VPB_MOUNTED 标志，则文件系统已装载卷。

3. 如果自系统启动以来文件系统尚未装载该卷（即，未设置 VPB_MOUNTED 标志），则 i/o 管理器会向每个可能声称该卷的文件系统发送卷装入（[**IRP_MJ_FILE_SYSTEM_CONTROL**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)，IRP_MN_MOUNT_VOLUME）请求。

   并非所有内置文件系统都一定会在系统启动后加载。 （请参阅[系统启动过程中对文件系统的影响](what-happens-to-file-systems-during-system-boot.md)。）对于尚未加载的内置文件系统，i/o 管理器会将卷装入请求发送到文件系统识别器（FsRec），这会代表这些文件系统检查卷引导扇区。

   如果 FsRec 确定卷是由尚未加载的文件系统格式化的，则 i/o 管理器会通过将加载文件系统（[**IRP_MJ_FILE_SYSTEM_CONTROL**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)、IRP_MN_LOAD_FILE_SYSTEM）请求发送到 FsRec 来做出响应，后者会加载文件系统。 然后，i/o 管理器将原始的卷装入请求发送到文件系统。

4. 每个接收装载卷请求的文件系统将检查卷的启动扇区，以确定卷的格式和其他信息是否指示该卷已由该特定文件系统格式化。 如果格式匹配，则文件系统会装载卷。

以下各节讨论文件系统在识别后如何装载卷：

[卷的装载方式](how-the-volume-is-mounted.md)

[卷装入示例](volume-mount-example.md)
