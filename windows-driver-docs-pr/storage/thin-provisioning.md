---
title: 精简预配
description: 精简预配
ms.assetid: 0D65DDCC-D207-4EA8-B5D6-56DF57221EE3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51beda233bada2573181343ee359a17f8c4f3c53
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543017"
---
# <a name="thin-provisioning"></a>精简预配


## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概述


精简预配是预配解决方案的端到端存储。 它还要求在主机和客户端应用程序上计划存储部署和执行。 Windows Server 精简预配功能用作精简预配支持的存储和主机服务器之间的接口。 精简预配功能包括精简预配的逻辑单元 (LUN) 标识、 的阈值通知、 资源耗尽的句柄和用于提供预配服务向最终用户的高可用性和可缩放存储空间回收。

## <a name="span-idthinprovisioninglunidentificationspanspan-idthinprovisioninglunidentificationspanspan-idthinprovisioninglunidentificationspanthin-provisioning-lun-identification"></a><span id="Thin_Provisioning_LUN_Identification"></span><span id="thin_provisioning_lun_identification"></span><span id="THIN_PROVISIONING_LUN_IDENTIFICATION"></span>精简设置 LUN 标识


Windows Server 已采用标识从 Windows Server 2012 的精简预配 Lun 的 T10 SCSI 块命令 3 (SBC3) 标准规范。 初始目标设备枚举，在 Windows Server 从目标设备中收集所有属性参数。 Windows Server 标识预配类型和 UNMAP 和修整功能。 存储设备将报告其预配类型和 UNMAP 和修整功能根据 SBC3 规范。

如果存储设备不会准确地报告其当前的功能，可能出现设备兼容性问题。 例如，如果存储设备报告它支持 UNMAP 命令，但它不支持 UNMAP 命令，可能会出现磁盘格式挂起问题。 准确设置类型信息时，存储堆栈可以提供更好的 I/O 处理根据预配类型的存储。

## <a name="span-idrun-timeprovisioningtypeorluncapacitychangesspanspan-idrun-timeprovisioningtypeorluncapacitychangesspanspan-idrun-timeprovisioningtypeorluncapacitychangesspanrun-time-provisioning-type-or-lun-capacity-changes"></a><span id="Run-time_Provisioning_Type_or_LUN_Capacity_Changes"></span><span id="run-time_provisioning_type_or_lun_capacity_changes"></span><span id="RUN-TIME_PROVISIONING_TYPE_OR_LUN_CAPACITY_CHANGES"></span>运行时设置类型或 LUN 容量更改


存储管理员可能会更改设置类型或 LUN 的容量。 当更改设置类型或 LUN 容量时，存储阵列引发单元关注有意义条件的检测数据请求时返回正确的信息。 若要预配类型或 LUN 容量更改的系统管理员发出警报的系统事件的 Windows 服务器日志。

## <a name="span-idthresholdandresourceexhaustionhandlesspanspan-idthresholdandresourceexhaustionhandlesspanspan-idthresholdandresourceexhaustionhandlesspanthreshold-and-resource-exhaustion-handles"></a><span id="Threshold_and_Resource_Exhaustion_Handles_"></span><span id="threshold_and_resource_exhaustion_handles_"></span><span id="THRESHOLD_AND_RESOURCE_EXHAUSTION_HANDLES_"></span>阈值和资源耗尽句柄


使用更少的物理大小的 LUN 的磁盘空间通常创建精简预配 LUN。 阈值通知是所需的函数发出警报的存储空间消耗状态的主机和客户端应用程序。 大多数的精简预配的存储阵列不报告事件时达到的阈值。 这些精简预配的存储解决方案解决其专有存储管理实用程序的阈值通知。 因此，对于主机和客户端应用程序，这些存储阵列报告是永久资源耗尽的唯一事件。 精简预配的存储设备可以使用的阈值通知句柄，临时资源耗尽句柄，或即将达到永久资源耗尽句柄警报系统管理员或客户端应用程序时消耗的存储空间容量。

### <a name="span-idthinprovisioningthresholdnotificationspanspan-idthinprovisioningthresholdnotificationspanspan-idthinprovisioningthresholdnotificationspanthin-provisioning-threshold-notification"></a><span id="Thin_Provisioning_Threshold_Notification"></span><span id="thin_provisioning_threshold_notification"></span><span id="THIN_PROVISIONING_THRESHOLD_NOTIFICATION"></span>精简设置的阈值通知

存储管理实用程序设置精简配置阈值。 Windows Server 不重写存储管理实用程序设置的阈值。 对于精简设置 LUN，存储管理员必须指定根据平均存储使用率阈值。 写入命令有超过存储目标设备已设置的阈值，目标设备通过使用有意义的数据来终止命令并将发送"精简设置软阈值达到"消息。 在 Windows Server 接收匹配的检测数据，将发生以下情况：

-   系统事件记录要 LUN 设备已达到资源使用情况或可用性阈值主机管理员发出警报。
-   在系统事件日志中有关从目标设备的日志页的已用和可用映射资源报告信息。 为此，存储阵列必须支持逻辑块的预配 Windows 服务器，以生成系统事件日志页规范。
-   终止的命令重试。

**请注意**  编写命令发送后将记录此错误可能可能会丢失如果文件\_标志\_编写\_THROUGH 不设置，因为它们可能会触发的永久资源耗尽情况。

 

### <a name="span-idtemporaryresourceexhaustionspanspan-idtemporaryresourceexhaustionspanspan-idtemporaryresourceexhaustionspantemporary-resource-exhaustion"></a><span id="Temporary_Resource_Exhaustion"></span><span id="temporary_resource_exhaustion"></span><span id="TEMPORARY_RESOURCE_EXHAUSTION"></span>临时资源耗尽

如果存储阵列启用自动增长的 LUN 上的函数，管理员可以使用临时资源耗尽的情况通知来确保存储设备可以四秒内对 LUN 分配了额外的空间。 当写入命令导致的临时资源耗尽情况时，存储设备终止请求该操作使用有意义的数据，并返回"空间分配正在进行"的消息的命令。 临时资源耗尽的情况进行处理，如下所示：

-   使用设置为 1 秒的重试间隔四次重试原始请求。
-   如果所有重试失败，则请求将返回到应用程序失败。
-   如果存储设备不处理临时资源耗尽，Windows Server 需要通过返回永久资源耗尽状态失败的下一个写请求的存储设备。

### <a name="span-idpermanentresourceexhaustionspanspan-idpermanentresourceexhaustionspanspan-idpermanentresourceexhaustionspanpermanent-resource-exhaustion"></a><span id="Permanent__Resource_Exhaustion"></span><span id="permanent__resource_exhaustion"></span><span id="PERMANENT__RESOURCE_EXHAUSTION"></span>永久资源耗尽

永久资源耗尽情况指示精简预配 LUN 已达到最大存储空间限制。 如果写入命令期间发生永久资源耗尽，存储设备通过使用有意义的数据来终止操作并发送"空间分配失败写入保护"消息。 永久耗尽的情况进行处理，如下所示：

-   如果原始请求的文件\_标志\_编写\_通过组，然后它故障回复到该应用程序。
-   如果原始请求不具有文件\_标志\_编写\_通过组，然后在应用程序可能会收到成功响应请求而完成，也不刷新到物理介质。
-   系统事件记录，其中包括"永久资源耗尽"错误消息。
-   错误代码传递回的分区管理器，并使 LUN 脱机。

## <a name="span-idstoragespacereclamationusingtheunmapcommandspanspan-idstoragespacereclamationusingtheunmapcommandspanspan-idstoragespacereclamationusingtheunmapcommandspanstorage-space-reclamation-using-the-unmap-command"></a><span id="Storage_Space_Reclamation_Using_the_UNMAP_Command"></span><span id="storage_space_reclamation_using_the_unmap_command"></span><span id="STORAGE_SPACE_RECLAMATION_USING_THE_UNMAP_COMMAND"></span>存储空间回收使用 UNMAP 命令


删除文件、 文件系统级别剪裁或存储优化操作会触发空间回收。 Trim 或 unmap 操作后，文件系统级别剪裁可用于设计为执行"读取返回零"的存储设备。

### <a name="span-idspacereclamationoperationinthestoragestackspanspan-idspacereclamationoperationinthestoragestackspanspan-idspacereclamationoperationinthestoragestackspanspace-reclamation-operation-in-the-storage-stack"></a><span id="Space_Reclamation_Operation_in_the_Storage_Stack"></span><span id="space_reclamation_operation_in_the_storage_stack"></span><span id="SPACE_RECLAMATION_OPERATION_IN_THE_STORAGE_STACK"></span>存储堆栈中的空间回收操作

当从文件系统中删除较大的文件或文件系统级别剪裁触发时，Windows Server 将相应的 UNMAP 请求转换为文件删除或剪裁通知。 存储端口驱动程序堆栈将 UNMAP 请求转换成 SCSI 取消映射的命令或存储设备的协议类型根据 ATA 剪裁命令。 在存储设备枚举，Windows 存储堆栈收集有关存储设备是否支持 UNMAP 或 TRIM 命令的信息。 如果设备具有 SCSI 取消映射或 ATA 剪裁功能仅 UNMAP 请求发送到存储设备。 Windows Server 还为存储目标设备上取消映射 LBAs 提供 API 实现。 Windows Server 不采用 T10 SCSI 编写相同的命令集。

### <a name="span-idunmaprequestsfromthehyper-vguestoperatingsystemspanspan-idunmaprequestsfromthehyper-vguestoperatingsystemspanspan-idunmaprequestsfromthehyper-vguestoperatingsystemspanunmap-requests-from-the-hyper-v-guest-operating-system"></a><span id="UNMAP_Requests_from_the_Hyper-V_Guest_Operating_System"></span><span id="unmap_requests_from_the_hyper-v_guest_operating_system"></span><span id="UNMAP_REQUESTS_FROM_THE_HYPER-V_GUEST_OPERATING_SYSTEM"></span>取消映射来自 HYPER-V 来宾操作系统的请求

在虚拟机 (VM) 创建过程的 HYPER-V 主机发送有关是查询虚拟硬盘 (VHD) 所在的存储设备支持 UNMAP 或 TRIM 命令。 当从 VM 来宾操作系统的文件系统删除大型文件时，来宾操作系统将文件删除请求发送到虚拟机的虚拟硬盘 (VHD) 或 VHD 文件。 VM 的 VHD 或 VHD 文件的隧道类驱动程序堆栈的 Windows 的 HYPER-V 主机，SCSI 取消请求，如下所示：

-   如果 VM 有一个 VHD，VHD 将 SCSI 取消映射或 ATA 剪裁命令转换成数据集管理 I/O 控制 (IOCTL DSM) 代码 TRIM 请求，然后将请求发送到主机存储设备。
-   如果 VM 有 VHD 文件，VHD 文件系统 SCSI 取消映射或 ATA 剪裁命令转换为文件系统级别剪裁请求，然后将请求发送到主机操作系统。

Windows HYPER-V 还支持从来宾操作系统 IOCTL DSM 修整的调用。

### <a name="span-idwindowsoptimizedrivesutilityspanspan-idwindowsoptimizedrivesutilityspanspan-idwindowsoptimizedrivesutilityspanwindows-optimize-drives-utility"></a><span id="Windows_Optimize_Drives_Utility"></span><span id="windows_optimize_drives_utility"></span><span id="WINDOWS_OPTIMIZE_DRIVES_UTILITY"></span>Windows 优化驱动器实用程序

最终用户或系统管理员可以使用优化驱动器实用程序以回收空间，通过创建手动请求或优化计划配置。 如果磁盘驱动器的精简设置 LUN，磁盘驱动器的媒体类型将显示为"精简预配驱动器"。

系统管理员可以使用优化驱动器实用程序来计划存储空间合并。 该实用工具还可以通知系统管理员，如果系统未命中三个连续计划运行。

## <a name="span-idretrievingtheslabmappingstatespanspan-idretrievingtheslabmappingstatespanspan-idretrievingtheslabmappingstatespanretrieving-the-slab-mapping-state"></a><span id="Retrieving_the_Slab_Mapping_State"></span><span id="retrieving_the_slab_mapping_state"></span><span id="RETRIEVING_THE_SLAB_MAPPING_STATE"></span>检索碎片映射状态


在精简设置 LUN，所有逻辑块都组织在 slabs （群集）。 碎片大小由存储设备报告的最佳取消映射粒度参数设置。 所有 slabs 都分为映射、 解除分配或锚定的状态。 Windows Server 将解除分配和锚定状态视为未映射的状态。 Windows Server 提供了一个 API 实现或 IOCTL DSM 分配，若要从为存储管理操作的精简预配 Lun 检索 LBA 预配状态。 应用程序可以调用 IOCTL DSM 分配例程以发送的 SCSI 命令和检索特定范围内的每个碎片的映射或未映射的状态。 如果预配状态返回 LBA 不描述整个分配范围，应用程序将发送另一个 SCSI 命令来检索剩余 LBA 范围的设置状态。

存储设备不需要处理整个 LBA 范围中返回。 如果返回的原始请求的部分 LBA 范围，发送另一个命令检索剩余 LBA 范围的映射状态。

 

 




