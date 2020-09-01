---
title: 常规存储 I/O 控制代码
description: 描述存储设备经常需要的一组标准服务和随附的设备控制代码。
keywords:
- 存储驱动程序 WDK 存储
- wdk cd-rom 驱动程序
- IOCTLs WDK cd-rom
ms.date: 12/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: 83fe120d3aebbf917ff886297b05e73fd23b5401
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185459"
---
# <a name="general-storage-io-control-codes"></a>常规存储 I/O 控制代码

不同类型的存储设备通常需要相同的服务。 此部分不会重复为每种设备类型提供这些服务的 IOCTL 请求，而是定义一组标准服务以及存储设备经常需要的随附设备控制代码。 此处定义的 i/o 控制代码的格式 IOCTL_STORAGE_*XXX* ，它们取代了 IOCTL_*DeviceType_XXX* 控制代码，其中 *DeviceType* 是磁盘、磁带或 CDROM。 例如， **IOCTL_STORAGE_RESERVE** 替换 **IOCTL_DISK_RESERVE**、 **IOCTL_TAPE_RESERVE**和 **IOCTL_CDROM_RESERVE**。 IOCTL_STORAGE_*XXX* 控制代码对函数代码、传输方法和所需访问的值相同，如以前的磁盘、磁带和 cd-rom 代码。 唯一的区别是设备类型。

存储类驱动程序会启动其中一些请求，但通常是这样的应用程序。 存储类驱动程序必须处理这些请求中的部分或全部，具体取决于存储设备的类型。 如果不存在存储类驱动程序，应用程序可能会直接向端口驱动程序发出请求。

|IOCTL|描述|
|----|----|
|[IOCTL_STORAGE_BREAK_RESERVATION](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_break_reservation)|中断磁盘保留。|
|[IOCTL_STORAGE_CHECK_VERIFY](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_check_verify)|确定在调用方打开以进行读取或写入访问的可移动媒体设备上，媒体是否已更改。|
|[IOCTL_STORAGE_CHECK_VERIFY2](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_check_verify2)|确定媒体是否已在可移动介质设备上更改-调用方已使用 **FILE_READ_ATTRIBUTES**打开。|
|[IOCTL_STORAGE_DEVICE_POWER_CAP](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_device_power_cap)|指定存储设备的最高运行功率消耗级别。|
|[IOCTL_STORAGE_EJECT_MEDIA](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_eject_media)|如果设备支持弹出功能，则导致设备弹出媒体。|
|[IOCTL_STORAGE_EJECTION_CONTROL](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_ejection_control)|锁定设备以防介质被删除。|
|[IOCTL_STORAGE_FIND_NEW_DEVICES](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_find_new_devices)|确定驱动程序支持的另一台设备是否已连接到 i/o 总线，自系统启动以来或自驱动程序上次处理此请求以来。|
|[IOCTL_STORAGE_FIRMWARE_ACTIVATE](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_firmware_activate)|激活存储设备上的固件映像。|
|[IOCTL_STORAGE_FIRMWARE_DOWNLOAD](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_firmware_download)|将固件映像下载到存储设备，但不会将其激活。|
|[IOCTL_STORAGE_FIRMWARE_GET_INFO](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_firmware_get_info)|查询存储设备以获取详细的固件信息。|
|[IOCTL_STORAGE_GET_DEVICE_NUMBER](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_device_number)|返回一个 **STORAGE_DEVICE_NUMBER** 结构，该结构包含分区设备的 FILE_DEVICE_XXX 类型、设备号，以及设备启动时由驱动程序分配给设备的分区号。|
|[IOCTL_STORAGE_GET_HOTPLUG_INFO](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_hotplug_info)|检索指定设备的热配置。|
|[IOCTL_STORAGE_GET_LB_PROVISIONING_MAP_RESOURCES](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_lb_provisioning_map_resources)|**IOCTL_STORAGE_GET_LB_PROVISIONING_MAP_RESOURCES**请求将发送到存储类驱动程序，以确定存储设备上的可用和已用映射资源。|
|[IOCTL_STORAGE_GET_MEDIA_SERIAL_NUMBER](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_media_serial_number)|查询 usb 通用父驱动程序的 USB 设备序列号。|
|[IOCTL_STORAGE_GET_MEDIA_TYPES](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_media_types)|返回有关软盘驱动器的几何信息。|
|[IOCTL_STORAGE_GET_MEDIA_TYPES_EX](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_media_types_ex)|返回有关设备支持的媒体类型的信息。|
|[IOCTL_STORAGE_GET_PHYSICAL_ELEMENT_STATUS](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_physical_element_status)|**IOCTL_STORAGE_GET_PHYSICAL_ELEMENT_STATUS**控制代码查询并返回设备的物理元素状态。|
|[IOCTL_STORAGE_LOAD_MEDIA](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_load_media)|导致在调用方打开以进行读取或写入访问的设备中加载媒体。|
|[IOCTL_STORAGE_LOAD_MEDIA2](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_load_media2)|使媒体加载到调用方已使用 **FILE_READ_ATTRIBUTES**打开的设备中。|
|[IOCTL_STORAGE_MANAGE_DATA_SET_ATTRIBUTES](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_manage_data_set_attributes)|此 **IOCTL_STORAGE_MANAGE_DATA_SET_ATTRIBUTES** 请求用于将管理数据集属性请求发送到存储设备。|
|[IOCTL_STORAGE_MCN_CONTROL](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_mcn_control)|暂时启用或禁用在可移动媒体设备上 **GUID_IO_MEDIA_ARRIVAL** 和 **GUID_IO_MEDIA_REMOVAL** 的自定义 PnP 事件传递。|
|[IOCTL_STORAGE_MEDIA_REMOVAL](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_media_removal)|锁定设备以防介质被删除。|
|[IOCTL_STORAGE_PERSISTENT_RESERVE_IN](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_persistent_reserve_in)| ( # A0) 的泛型存储类驱动程序公开 i/o 控制 (IOCTL) 接口，以便在命令中发出持久保留。|
|[IOCTL_STORAGE_PERSISTENT_RESERVE_OUT](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_persistent_reserve_out)| ( # A0) 的泛型存储类驱动程序公开了一个 i/o 控件 (IOCTL) 接口，用于发出持久的保留输出命令。|
|[IOCTL_STORAGE_PREDICT_FAILURE](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_predict_failure)|轮询设备故障预测。|
|[IOCTL_STORAGE_PROTOCOL_COMMAND](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command)|驱动程序可以使用 **IOCTL_STORAGE_PROTOCOL_COMMAND** 将特定于供应商的命令传递到存储设备|
|[IOCTL_STORAGE_QUERY_PROPERTY](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)|驱动程序可以使用 **IOCTL_STORAGE_QUERY_PROPERTY** 来返回存储设备或适配器的属性。|
|[IOCTL_STORAGE_READ_CAPACITY](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_read_capacity)|**IOCTL_STORAGE_READ_CAPACITY**请求返回目标存储设备的读取容量信息。|
|[IOCTL_STORAGE_REINITIALIZE_MEDIA](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_reinitialize_media)|驱动程序可以使用 **IOCTL_STORAGE_REINITIALIZE_MEDIA** 控制代码来重新初始化或擦除设备。|
|[IOCTL_STORAGE_RELEASE](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_release)|释放先前保留的设备，以在支持多个发起程序的总线上独占使用调用方，并使用保留设备的概念（如 SCSI 总线）。|
|[IOCTL_STORAGE_RESERVE](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_reserve)|声明一个设备，用于在支持多个发起程序的总线上独占使用调用方，并为保留设备的概念（如 SCSI 总线）声明。|
|[IOCTL_STORAGE_RESET_BUS](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_reset_bus)|重置总线上的每个设备，并将其间接重置。|
|[IOCTL_STORAGE_RESET_DEVICE](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_reset_device)|如果可能，将重置非 SCSI 存储设备，而不影响总线上的其他设备。|
|[IOCTL_STORAGE_SET_HOTPLUG_INFO](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_set_hotplug_info)|设置指定设备的热配置。|
|[IOCTL_STORAGE_SET_PROPERTY](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_set_property)|指示更改属性的请求是成功还是导致错误。
|[IOCTL_STORAGE_SET_TEMPERATURE_THRESHOLD](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_set_temperature_threshold)|当硬件) 支持时，驱动程序可以使用 **IOCTL_STORAGE_SET_TEMPERATURE_THRESHOLD** 设置存储设备 (的温度阈值。|