---
title: CD-ROM I/O 控制代码
description: CD-ROM 设备的类驱动程序处理其他公共的 I/O 控制代码，本主题中所述。
keywords:
- CD-ROM 驱动程序 WDK 存储
- Ioctl WDK CD-ROM
ms.date: 12/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8dbff0e504ed489843bba098ceaba315ecaa7b4c
ms.sourcegitcommit: a678a339f09fbd56a3a6124c0fe86194fedb2ed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2019
ms.locfileid: "57560623"
---
# <a name="cd-rom-io-control-codes"></a>CD-ROM I/O 控制代码

所有公共的 I/O 控制代码的 CD-ROM 的设备驱动程序使用缓冲的 I/O。 因此，输入或输出数据的这些请求位于 Irp-> AssociatedIrp.SystemBuffer。

CD-ROM 设备的类驱动程序处理其他公共 I/O 控制代码，以及与那些在本部分中所述。 有关存储类驱动程序要求的详细信息，请参阅[常规存储 I/O 控制代码](general-storage-io-control-codes.md)。

|I/O 控制代码|描述|
|----|----|
|[IOCTL_CDROM_CHECK_VERIFY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_check_verify)|替换为此 IOCTL [IOCTL_STORAGE_CHECK_VERIFY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_check_verify)。 两个 Ioctl 之间的唯一区别是基础值。|
|**IOCTL_CDROM_CLOSE_DOOR**|此 I/O 控制代码已被取代[IOCTL_STORAGE_LOAD_MEDIA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_load_media)。|
|[IOCTL_CDROM_ENABLE_STREAMING](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_enable_streaming)|启用或禁用 CDROM 为原始读取和写入请求流模式在每个句柄的基础上。 若要执行此操作，调用**DeviceIoControl**函数，并指定**IOCTL_CDROM_ENABLE_STREAMING**作为的 I/O 控制请求*dwIoControlCode*参数。|
|[IOCTL_CDROM_EXCLUSIVE_ACCESS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_exclusive_access)|指示 CD-ROM 类驱动程序导出 CD-ROM 设备访问状态、 独占访问权限，将 CD-ROM 设备锁定和解锁 CD-ROM 设备进行独占访问。|
|[IOCTL_CDROM_FIND_NEW_DEVICES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_find_new_devices)|替换为此 IOCTL [IOCTL_STORAGE_FIND_NEW_DEVICES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_find_new_devices)。 两个 Ioctl 之间的唯一区别是基础值。|
|[IOCTL_CDROM_GET_CONFIGURATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_configuration)|请求从 CD-ROM 设备功能和配置文件信息。|
|[IOCTL_CDROM_GET_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_control)|此 IOCTL 请求已过时。 不使用。|
|[IOCTL_CDROM_GET_DRIVE_GEOMETRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_drive_geometry)|返回有关 CD ROM 的几何图形 （媒体类型的圆柱体数目、 每柱面磁道数，每个音轨，扇区和每个扇区字节） 的信息。|
|[IOCTL_CDROM_GET_DRIVE_GEOMETRY_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_drive_geometry_ex)|返回有关 CD-ROM 的几何图形 （媒体类型的圆柱体数目、 每柱面磁道数，每个音轨，扇区和每个扇区字节） 的信息。|
|[IOCTL_CDROM_GET_INQUIRY_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_inquiry_data)|返回 CD-ROM 设备的 SCSI 查询数据。 使用以独占方式锁定了设备时，可以使用此 IOCTL [IOCTL_CDROM_EXCLUSIVE_ACCESS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_exclusive_access)。|
|[IOCTL_CDROM_GET_LAST_SESSION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_last_session)|查询设备的第一个完整的会话数、 最后一个完整的会话数和最后一个完成会话起始地址。|
|[IOCTL_CDROM_GET_PERFORMANCE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_performance)|从设备检索受支持的速度。 **IOCTL_CDROM_GET_PERFORMANCE** I/O 控制请求是通过 MMC 命令，获取性能的包装器。|
|[IOCTL_CDROM_GET_VOLUME](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_volume)|已过时。 确定在当前卷的每个其设备的音频端口。|
|[IOCTL_CDROM_LOAD_MEDIA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_load_media)|插入驱动器重新绘制 protruding CDROM 送纸器。|
|[IOCTL_CDROM_PAUSE_AUDIO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_pause_audio)|已过时。 暂停音频播放。|
|[IOCTL_CDROM_PLAY_AUDIO_MSF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_play_audio_msf)|已过时。 播放媒体的指定的范围。|从 cd-rom 放入 raw 模式读取数据。|
|[IOCTL_CDROM_READ_Q_CHANNEL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_read_q_channel)|已过时。 返回当前的位置、 媒体目录或 ISRC 跟踪数据。|
|[IOCTL_CDROM_READ_TOC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_read_toc)|已过时。 返回的媒体内容的表。|
|[IOCTL_CDROM_READ_TOC_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_read_toc_ex)|查询目录 (toc)、 程序的内存区域 (PMA) 和 pregroove (ATIP) 中的绝对时间的目标设备。|
|[IOCTL_CDROM_RESUME_AUDIO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_resume_audio)|已过时。 恢复挂起的音频操作。|
|[IOCTL_CDROM_SEEK_AUDIO_MSF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_seek_audio_msf)|已过时。 在媒体上将移动到指定的 MSF 在标题之下。|
|[IOCTL_CDROM_SEND_OPC_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_send_opc_information)|在文件系统和想要提前执行最佳 Power 校准 (OPC) 过程，以便不需要等待完成的过程的第一个流写入其他实现中使用。|
|[IOCTL_CDROM_SET_SPEED](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_set_speed)|设置主轴转速的 CD-ROM 驱动器。|
|[IOCTL_CDROM_SET_VOLUME](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_set_volume)|已过时。 重置为其设备的音频端口的卷。|
|[IOCTL_CDROM_STOP_AUDIO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_stop_audio)|已过时。 结束音频播放。|
