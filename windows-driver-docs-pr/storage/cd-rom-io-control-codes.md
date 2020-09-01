---
title: CD-ROM I/O 控制代码
description: Cd-rom 设备的类驱动程序处理其他公共 i/o 控制代码，如本主题中所述。
keywords:
- CD-ROM 驱动程序 WDK 存储
- IOCTLs WDK cd-rom
ms.date: 12/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2ec0b20441e2afead95dd5d901fec4800e606f5a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191322"
---
# <a name="cd-rom-io-control-codes"></a>CD-ROM I/O 控制代码

Cd-rom 设备驱动程序的所有公共 i/o 控制代码均使用缓冲 i/o。 因此，这些请求的输入或输出数据位于 >AssociatedIrp.SystemBuffer 中。

Cd-rom 设备的类驱动程序处理额外的公共 i/o 控制代码，以及本节所述的代码。 有关存储类驱动程序要求的详细信息，请参阅 [常规存储 I/o 控制代码](general-storage-io-control-codes.md)。

|I/o 控制代码|描述|
|----|----|
|[IOCTL_CDROM_CHECK_VERIFY](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_check_verify)|此 IOCTL 由 [IOCTL_STORAGE_CHECK_VERIFY](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_check_verify)替换。 这两个 IOCTLs 之间的唯一差别在于基值。|
|**IOCTL_CDROM_CLOSE_DOOR**|已 [IOCTL_STORAGE_LOAD_MEDIA](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_load_media)替换此 i/o 控制代码。|
|[IOCTL_CDROM_ENABLE_STREAMING](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_enable_streaming)|针对原始读写请求，启用或禁用每句柄的 CDROM 流模式。 若要执行此操作，请调用 **DeviceIoControl** 函数并将 **IOCTL_CDROM_ENABLE_STREAMING** i/o 控制请求指定为 *dwIoControlCode* 参数。|
|[IOCTL_CDROM_EXCLUSIVE_ACCESS](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_exclusive_access)|指示 cd-rom 类驱动程序导出 cd-rom 设备的访问状态，锁定 cd-rom 设备以进行独占访问，并解锁 cd-rom 设备以进行独占访问。|
|[IOCTL_CDROM_FIND_NEW_DEVICES](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_find_new_devices)|此 IOCTL 由 [IOCTL_STORAGE_FIND_NEW_DEVICES](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_find_new_devices)替换。 这两个 IOCTLs 之间的唯一差别在于基值。|
|[IOCTL_CDROM_GET_CONFIGURATION](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_configuration)|从 cd-rom 设备请求功能和配置文件信息。|
|[IOCTL_CDROM_GET_CONTROL](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_control)|此 IOCTL 请求已过时。 请勿使用。|
|[IOCTL_CDROM_GET_DRIVE_GEOMETRY](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_drive_geometry)|返回有关 CD-ROM 的几何信息 (媒体类型、柱面数、每个柱面的扇区、每个磁道的扇区和每个扇区的字节数) 。|
|[IOCTL_CDROM_GET_DRIVE_GEOMETRY_EX](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_drive_geometry_ex)|返回有关 CD-ROM 的几何信息 (媒体类型、柱面数、每个柱面的扇区、每个扇区的扇区和每个扇区的字节数) 。|
|[IOCTL_CDROM_GET_INQUIRY_DATA](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_inquiry_data)|返回 cd-rom 设备的 SCSI 查询数据。 当使用 [IOCTL_CDROM_EXCLUSIVE_ACCESS](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_exclusive_access)以独占方式锁定设备时，可以使用此 IOCTL。|
|[IOCTL_CDROM_GET_LAST_SESSION](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_last_session)|查询设备以查找第一个完整会话编号、最后一个完整会话编号以及最后一个完成会话起始地址。|
|[IOCTL_CDROM_GET_PERFORMANCE](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_performance)|检索设备支持的速度。 **IOCTL_CDROM_GET_PERFORMANCE** i/o 控制请求是 MMC 命令的包装器，可获取性能。|
|[IOCTL_CDROM_GET_VOLUME](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_volume)|已过时。 确定其每个设备的音频端口的当前卷。|
|[IOCTL_CDROM_LOAD_MEDIA](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_load_media)|将 protruding CDROM 托盘移回驱动器。|
|[IOCTL_CDROM_PAUSE_AUDIO](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_pause_audio)|已过时。 暂停播放音频。|
|[IOCTL_CDROM_PLAY_AUDIO_MSF](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_play_audio_msf)|已过时。 播放指定范围的媒体。|从 cd-rom 中读取原始模式下的数据。|
|[IOCTL_CDROM_READ_Q_CHANNEL](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_read_q_channel)|已过时。 返回当前位置、media catalog 或 ISRC track 数据。|
|[IOCTL_CDROM_READ_TOC](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_read_toc)|已过时。 返回媒体的目录。|
|[IOCTL_CDROM_READ_TOC_EX](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_read_toc_ex)|在目标设备上查询目录 (TOC) 、program memory area (PMA) 和 pregroove (ATIP) 中的绝对时间。|
|[IOCTL_CDROM_RESUME_AUDIO](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_resume_audio)|已过时。 恢复暂停的音频操作。|
|[IOCTL_CDROM_SEEK_AUDIO_MSF](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_seek_audio_msf)|已过时。 将标题移到媒体上的指定 MSF。|
|[IOCTL_CDROM_SEND_OPC_INFORMATION](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_send_opc_information)|在文件系统和其他实现中使用，这些实现提前 (OPC) 过程进行最佳的性能校准，使第一次流式处理写入无需等待过程完成。|
|[IOCTL_CDROM_SET_SPEED](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_set_speed)|设置 cd-rom 驱动器的磁盘轴速度。|
|[IOCTL_CDROM_SET_VOLUME](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_set_volume)|已过时。 重置设备的音频端口的卷。|
|[IOCTL_CDROM_STOP_AUDIO](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_stop_audio)|已过时。 结束音频播放。|