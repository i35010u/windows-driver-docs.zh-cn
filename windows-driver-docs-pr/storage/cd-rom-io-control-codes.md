---
title: CD-ROM I/O 控制代码
description: Cd-rom 设备的类驱动程序处理其他公共 i/o 控制代码，如本主题中所述。
keywords:
- CD-ROM 驱动程序 WDK 存储
- IOCTLs WDK cd-rom
ms.date: 12/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0c1fcaabcefc3a78f98b7dd57c8f643bca35aacd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841631"
---
# <a name="cd-rom-io-control-codes"></a>CD-ROM I/O 控制代码

Cd-rom 设备驱动程序的所有公共 i/o 控制代码均使用缓冲 i/o。 因此，这些请求的输入或输出数据位于 Irp-> AssociatedIrp. SystemBuffer。

Cd-rom 设备的类驱动程序处理额外的公共 i/o 控制代码，以及本节所述的代码。 有关存储类驱动程序要求的详细信息，请参阅[常规存储 I/o 控制代码](general-storage-io-control-codes.md)。

|I/o 控制代码|描述|
|----|----|
|[IOCTL_CDROM_CHECK_VERIFY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_check_verify)|此 IOCTL 将替换为[IOCTL_STORAGE_CHECK_VERIFY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_check_verify)。 这两个 IOCTLs 之间的唯一差别在于基值。|
|**IOCTL_CDROM_CLOSE_DOOR**|此 i/o 控制代码已被[IOCTL_STORAGE_LOAD_MEDIA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_load_media)替换。|
|[IOCTL_CDROM_ENABLE_STREAMING](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_enable_streaming)|针对原始读写请求，启用或禁用每句柄的 CDROM 流模式。 若要执行此操作，请调用**DeviceIoControl**函数并将**IOCTL_CDROM_ENABLE_STREAMING** i/o 控制请求指定为*dwIoControlCode*参数。|
|[IOCTL_CDROM_EXCLUSIVE_ACCESS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_exclusive_access)|指示 cd-rom 类驱动程序导出 cd-rom 设备的访问状态，锁定 cd-rom 设备以进行独占访问，并解锁 cd-rom 设备以进行独占访问。|
|[IOCTL_CDROM_FIND_NEW_DEVICES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_find_new_devices)|此 IOCTL 将替换为[IOCTL_STORAGE_FIND_NEW_DEVICES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_find_new_devices)。 这两个 IOCTLs 之间的唯一差别在于基值。|
|[IOCTL_CDROM_GET_CONFIGURATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_configuration)|从 cd-rom 设备请求功能和配置文件信息。|
|[IOCTL_CDROM_GET_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_control)|此 IOCTL 请求已过时。 不使用。|
|[IOCTL_CDROM_GET_DRIVE_GEOMETRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_drive_geometry)|返回有关 CD-ROM 的几何信息（媒体类型、柱面数、每个柱面的每个轨迹、每个扇区的扇区和每个扇区的字节数）。|
|[IOCTL_CDROM_GET_DRIVE_GEOMETRY_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_drive_geometry_ex)|返回有关 CD-ROM 的几何信息（媒体类型、柱面数、每个柱面的每个轨迹、每个扇区的扇区和每个扇区的字节数）。|
|[IOCTL_CDROM_GET_INQUIRY_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_inquiry_data)|返回 cd-rom 设备的 SCSI 查询数据。 当使用[IOCTL_CDROM_EXCLUSIVE_ACCESS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_exclusive_access)以独占方式锁定设备时，可以使用此 IOCTL。|
|[IOCTL_CDROM_GET_LAST_SESSION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_last_session)|查询设备以查找第一个完整会话编号、最后一个完整会话编号以及最后一个完成会话起始地址。|
|[IOCTL_CDROM_GET_PERFORMANCE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_performance)|检索设备支持的速度。 **IOCTL_CDROM_GET_PERFORMANCE** i/o 控制请求是 MMC 命令的包装器，可获取性能。|
|[IOCTL_CDROM_GET_VOLUME](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_volume)|已过时。 确定其每个设备的音频端口的当前卷。|
|[IOCTL_CDROM_LOAD_MEDIA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_load_media)|将 protruding CDROM 托盘移回驱动器。|
|[IOCTL_CDROM_PAUSE_AUDIO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_pause_audio)|已过时。 暂停播放音频。|
|[IOCTL_CDROM_PLAY_AUDIO_MSF](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_play_audio_msf)|已过时。 播放指定范围的媒体。|从 cd-rom 中读取原始模式下的数据。|
|[IOCTL_CDROM_READ_Q_CHANNEL](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_read_q_channel)|已过时。 返回当前位置、media catalog 或 ISRC track 数据。|
|[IOCTL_CDROM_READ_TOC](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_read_toc)|已过时。 返回媒体的目录。|
|[IOCTL_CDROM_READ_TOC_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_read_toc_ex)|在目标设备上查询目录（TOC）、程序内存区域（PMA）和 pregroove （ATIP）中的绝对时间。|
|[IOCTL_CDROM_RESUME_AUDIO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_resume_audio)|已过时。 恢复暂停的音频操作。|
|[IOCTL_CDROM_SEEK_AUDIO_MSF](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_seek_audio_msf)|已过时。 将标题移到媒体上的指定 MSF。|
|[IOCTL_CDROM_SEND_OPC_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_send_opc_information)|在需要提前执行最佳电源校准（OPC）过程的文件系统和其他实现中使用，以便第一次流式处理写入无需等待过程完成。|
|[IOCTL_CDROM_SET_SPEED](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_set_speed)|设置 cd-rom 驱动器的磁盘轴速度。|
|[IOCTL_CDROM_SET_VOLUME](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_set_volume)|已过时。 重置设备的音频端口的卷。|
|[IOCTL_CDROM_STOP_AUDIO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_stop_audio)|已过时。 结束音频播放。|
