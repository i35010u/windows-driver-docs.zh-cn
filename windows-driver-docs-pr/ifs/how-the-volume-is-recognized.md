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
ms.openlocfilehash: 7c193b217fc4fc16a4ae84309487df61f3d9d245
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065948"
---
# <a name="how-the-volume-is-recognized"></a>如何识别卷

> [!NOTE]
> 为了获得最佳的可靠性和性能，请使用带有筛选器管理器支持的 [文件系统微筛选器驱动程序](./filter-manager-concepts.md) ，而不是使用旧的文件系统 若要将旧驱动程序移植到微筛选器驱动程序，请参阅 [迁移旧筛选器驱动程序的准则](guidelines-for-porting-legacy-filter-drivers.md)。

卷装入过程通常由在逻辑卷上打开文件的请求触发， (即分区或动态卷) ，如下所示：

1. 用户应用程序调用 **CreateFile** 来打开文件。 或内核模式驱动程序调用 [**ZwCreateFile**](/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile) 或 [**IoCreateFileSpecifyDeviceObjectHint**](/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)。

2. I/o 管理器确定请求的目标是哪个逻辑卷，并检查其设备对象以查看它是否已装入。 如果设置了 VPB_MOUNTED 标志，则文件系统已装载卷。

3. 如果文件系统由于系统 (启动而未装载卷（即，未将 VPB_MOUNTED 标志设置) ，则 i/o 管理器会将卷装入 ([**IRP_MJ_FILE_SYSTEM_CONTROL**](./irp-mj-file-system-control.md)IRP_MN_MOUNT_VOLUME) 请求发送到可能会声明该卷的每个文件系统。

   并非所有内置文件系统都一定会在系统启动后加载。  (查看 [系统启动过程中对文件系统的影响](what-happens-to-file-systems-during-system-boot.md)。 ) 对于尚未加载的内置文件系统，I/o 管理器会将卷装入请求发送到文件系统识别器 (FsRec) ，后者会代表这些文件系统检查卷引导扇区。

   如果 FsRec 确定卷是由尚未加载的文件系统格式化的，则 i/o 管理器会通过 [**IRP_MJ_FILE_SYSTEM_CONTROL**](./irp-mj-file-system-control.md) (发送负载文件系统进行响应，IRP_MN_LOAD_FILE_SYSTEM 将) 请求发送到 FsRec，后者会加载文件系统。 然后，i/o 管理器将原始的卷装入请求发送到文件系统。

4. 每个接收装载卷请求的文件系统将检查卷的启动扇区，以确定卷的格式和其他信息是否指示该卷已由该特定文件系统格式化。 如果格式匹配，则文件系统会装载卷。

以下各节讨论文件系统在识别后如何装载卷：

[卷的装载方式](how-the-volume-is-mounted.md)

[卷装入示例](volume-mount-example.md)