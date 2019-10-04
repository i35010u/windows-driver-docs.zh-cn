---
title: 精简预配
description: 精简预配
ms.assetid: 0D65DDCC-D207-4EA8-B5D6-56DF57221EE3
ms.date: 10/04/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6ec9e06dee020367291cb7207452f1b640a6e561
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71939092"
---
# <a name="thin-provisioning"></a>精简预配

## <a name="overview"></a>概述

精简设置是一种端到端存储预配解决方案，可提供实时分配。 它需要在主机和客户端应用程序上规划存储部署和执行。 Windows Server 精简设置功能充当精简预配支持的存储和主机服务器之间的接口。 精简设置功能包括精简预配逻辑单元（LUN）标识、阈值通知、资源耗尽的句柄和用于向最终用户提供高度可用且可缩放的存储预配服务的空间回收。

## <a name="thin-provisioning-lun-identification"></a>精简设置 LUN 标识

Windows Server 采用了用于标识从 Windows Server 2012 开始的精简预配 Lun 的 T10 SCSI 块命令3（SBC3）标准规范。 在初始目标设备枚举过程中，Windows Server 从目标设备收集所有属性参数。 Windows Server 标识预配类型和取消映射和剪裁功能。 根据 SBC3 规范，存储设备会报告其设置类型以及取消映射和剪裁功能。

如果存储设备无法准确报告其当前功能，可能会出现设备兼容性问题。 例如，如果存储设备报告它支持 "取消映射" 命令，但不支持 "取消映射" 命令，则可能出现磁盘格式挂起问题。 当预配类型信息准确时，存储堆栈可根据存储设置类型提供更好的 i/o 处理。

## <a name="run-time-provisioning-type-or-lun-capacity-changes"></a>运行时设置类型或 LUN 容量更改

存储管理员可以更改 LUN 的设置类型或容量。 当设置类型或 LUN 容量更改时，存储阵列将引发一个单元注意的条件，该条件在请求感知数据时返回正确的信息。 Windows Server 记录系统事件，以向系统管理员发出预配类型或 LUN 容量更改警报。

## <a name="threshold-and-resource-exhaustion-handles"></a>阈值和资源耗尽句柄

通常使用比 LUN 大小少的物理磁盘空间创建精简设置 LUN。 阈值通知是用于向主机和客户端应用程序发送存储空间消耗状态警报的必需函数。 达到阈值时，大多数精简设置存储阵列不会报告事件。 这些精简预配存储解决方案通过其专用存储管理实用工具解决了阈值通知。 因此，对于主机和客户端应用程序，这些存储阵列报告的唯一事件是永久资源耗尽。 精简预配存储设备可以使用阈值通知句柄、临时资源耗尽句柄或永久性资源耗尽句柄来在存储空间消耗接近时向系统管理员或客户端应用程序发出警报功能.

### <a name="thin-provisioning-threshold-notification"></a>精简设置阈值通知

存储管理实用工具设置精简设置阈值。 Windows Server 不会替代存储管理实用工具设置的阈值。 对于精简设置 LUN，存储管理员必须根据平均存储消耗费率指定阈值。 当写入命令超过存储目标设备设置的阈值时，目标设备将通过使用检测数据来终止命令并发送 "已达到精简设置软阈值" 消息。 当 Windows Server 接收到匹配的感知数据时，将发生以下情况：

- 将记录系统事件，以提醒主机管理员已在 LUN 设备上达到资源使用或可用性阈值。
- 在系统事件日志中，从目标设备的 "日志" 页报告有关已使用和可用映射的资源的信息。 为此，存储阵列必须支持逻辑块预配的日志页面规范，以便 Windows Server 生成系统事件。
- 已终止的命令将重试。

> [!NOTE]
> 如果未设置 FILE_FLAG_WRITE_THROUGH，则在记录该错误后发送的写入命令可能会丢失，因为它们可能会触发永久性资源耗尽情况。

### <a name="temporary-resource-exhaustion"></a>临时资源耗尽

当存储阵列在 LUN 上启用自动增长功能时，管理员可以使用临时资源耗尽通知来确保存储设备可以在四秒钟内向 LUN 分配额外空间。 当写入命令导致临时资源耗尽情况时，存储设备将终止使用感知数据请求操作的命令，并返回 "正在进行的空间分配" 消息。 临时资源耗尽的处理方式如下：

- 重试原始请求四次，重试间隔设置为1秒。
- 如果所有重试均失败，请求将故障回复到应用程序。
- 如果存储设备不能处理临时资源耗尽，Windows Server 会要求存储设备在下一次写入请求时，返回永久的资源耗尽状态。

### <a name="permanent-resource-exhaustion"></a>永久资源耗尽

永久资源耗尽情况表明精简设置 LUN 已经达到了最大存储空间限制。 当在写入命令期间发生永久性资源耗尽时，存储设备将通过使用 "感知数据" 终止操作，并发送 "空间分配失败写保护" 消息。 永久耗尽的处理方式如下：

- 如果原始请求已设置 FILE_FLAG_WRITE_THROUGH，则会故障回复到应用程序。
- 如果原始请求未设置 FILE_FLAG_WRITE_THROUGH，则在没有完成请求或未刷新到物理媒体的情况下，应用程序可能会收到成功响应。
- 将记录系统事件，其中包含 "永久资源耗尽" 错误消息。
- 错误代码将传回分区管理器，LUN 将脱机。

## <a name="storage-space-reclamation-using-the-unmap-command"></a>使用 "取消" 命令回收存储空间

可以通过文件删除、文件系统级别修整或存储优化操作来触发空间回收。 为设计为在修整或取消映射操作后执行 "读取返回零" 的存储设备启用文件系统级修整。

### <a name="space-reclamation-operation-in-the-storage-stack"></a>存储堆栈中的空间回收操作

当从文件系统中删除大文件或触发文件系统级别剪裁时，Windows Server 会将文件删除或剪裁通知转换为相应的取消请求。 存储端口驱动程序堆栈根据存储设备的协议类型将取消映射请求转换为 SCSI 取消命令或 ATA TRIM 命令。 在存储设备枚举过程中，Windows 存储堆栈会收集有关存储设备是否支持取消映射或剪裁命令的信息。 如果设备具有 SCSI 取消映射或 ATA 剪裁功能，则仅向存储设备发送取消请求。 Windows Server 还提供了用于在存储目标设备上取消映射 LBAs 的 API 实现。 Windows Server 不采用 T10 SCSI WRITE 相同的命令集。

### <a name="unmap-requests-from-the-hyper-v-guest-operating-system"></a>Hyper-v 来宾操作系统中的取消映射请求

在虚拟机（VM）创建期间，Hyper-v 主机会发送一个查询，该查询介绍虚拟硬盘（VHD）所在的存储设备是否支持取消映射或剪裁命令。 从 VM 来宾操作系统的文件系统中删除大文件时，来宾操作系统会将文件删除请求发送到虚拟机的虚拟硬盘（VHD）或 VHD 文件（或 VHDX 文件）。 VM 的 VHD 或 VHDX 文件向 Windows Hyper-v 主机的类驱动程序堆栈隧道进行 SCSI 取消映射请求，如下所示：

- 如果 VM 具有 VHD 文件，则 VHD 会将 SCSI 取消或 ATA 剪裁命令转换为[数据集管理 i/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/storage/data-set-management-overview)剪裁请求，然后将请求发送到主机存储设备。
- 如果 VM 有一个 VHDX 文件，则 VHD 文件系统会将 SCSI 取消映射或 ATA 剪裁命令转换为文件系统级剪裁请求，然后将请求发送到主机操作系统。

Windows Hyper-v 还支持来宾操作系统中的 IOCTL DSM 剪裁调用。

### <a name="windows-optimize-drives-utility"></a>Windows 优化驱动器实用工具

最终用户或系统管理员可以使用 "优化驱动器" 实用程序来通过创建手动请求或通过优化计划配置来回收空间。 如果磁盘驱动器是精简设置 LUN，则磁盘驱动器的媒体类型将显示为 "精简配置驱动器"。

系统管理员可以通过使用优化驱动器实用工具来计划存储空间合并。 如果系统未命中三个连续的计划运行，则该实用工具还可以通知系统管理员。

## <a name="retrieving-the-slab-mapping-state"></a>检索楼板映射状态

在精简设置 LUN 中，所有逻辑块都在碎片（群集）中进行分组。 平板大小由存储设备报告的最佳取消映射粒度参数设置。 所有碎片都分类为已映射的取消分配状态或锚定状态。 Windows Server 将取消分配状态和锚定状态视为未映射状态。 Windows Server 提供了一个 API 实现或 IOCTL DSM 分配，用于从精简设置 Lun 检索用于存储管理操作的 LBA 设置状态。 应用程序可以调用 IOCTL DSM 分配例程来发送 SCSI 命令，并检索特定范围内每个楼板的已映射或未映射状态。 如果返回的 LBA 预配状态不描述整个分配范围，则应用程序将发送另一个 SCSI 命令来检索剩余 LBA 范围的设置状态。

存储设备无需在一次返回时处理整个 LBA 范围。 如果已返回原始请求的部分 LBA 范围，则将发送另一个命令以检索剩余 LBA 范围的映射状态。
