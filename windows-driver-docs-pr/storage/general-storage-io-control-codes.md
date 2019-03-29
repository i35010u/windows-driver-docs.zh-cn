---
title: 常规存储 I/O 控制代码
description: 描述一组标准的服务和附带经常所需的存储设备的设备控制代码。
keywords:
- 存储驱动程序 WDK 存储
- wdk CD-ROM 驱动程序
- Ioctl WDK CD-ROM
ms.date: 12/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: a88d7928de2e519f2bb7bdc11462053aa29b5a64
ms.sourcegitcommit: a678a339f09fbd56a3a6124c0fe86194fedb2ed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2019
ms.locfileid: "57560624"
---
# <a name="general-storage-io-control-codes"></a>常规存储 I/O 控制代码

不同类型的存储设备通常需要相同的服务。 而不是重复的 IOCTL 请求提供这些服务的每种设备类型，此节定义一组标准的服务和附带经常所需的存储设备的设备控制代码。 在此处定义的 I/O 控制代码具有窗体 IOCTL_STORAGE_*XXX*并且它们替换 IOCTL_*DeviceType_XXX*控制代码，其中*DeviceType*是磁盘、 磁带或CDROM。 例如， **IOCTL_STORAGE_RESERVE**替换**IOCTL_DISK_RESERVE**， **IOCTL_TAPE_RESERVE**，以及**IOCTL_CDROM_RESERVE**。 IOCTL_STORAGE_*XXX*控制代码作为上一个磁盘、 磁带和 CD-ROM 代码具有相同的值的函数代码、 传输方法和所需的访问。 唯一的区别是设备类型。

存储类驱动程序将启动一些这些请求，但通常是执行操作的应用程序。 存储类驱动程序必须处理一些或所有这些请求，具体取决于存储设备的类型。 存在任何存储类驱动程序时，应用程序可能会直接向端口驱动程序发出请求。

|IOCTL|描述|
|----|----|
|[IOCTL_STORAGE_BREAK_RESERVATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_break_reservation)|将磁盘保留。|
|[IOCTL_STORAGE_CHECK_VERIFY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_check_verify)|确定媒体是否具有已更改的调用方已打开的读取或写入访问的可移动介质设备上。|
|[IOCTL_STORAGE_CHECK_VERIFY2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_check_verify2)|确定是否可移动介质设备上发生了变化媒体-调用方已打开与**FILE_READ_ATTRIBUTES**。|
|[IOCTL_STORAGE_DEVICE_POWER_CAP](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_device_power_cap)|指定的存储设备的最大可操作的电源消耗级别。|
|[IOCTL_STORAGE_EJECT_MEDIA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_eject_media)|导致要弹出的媒体，如果设备支持弹出功能的设备。|
|[IOCTL_STORAGE_EJECTION_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_ejection_control)|锁定设备，以防止删除媒体。|
|[IOCTL_STORAGE_FIND_NEW_DEVICES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_find_new_devices)|确定是否该驱动程序支持的另一台设备已连接到的 I/O 总线，因为系统已启动或自上次处理此请求的驱动程序。|
|[IOCTL_STORAGE_FIRMWARE_ACTIVATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_firmware_activate)|激活的存储设备上的固件映像。|
|[IOCTL_STORAGE_FIRMWARE_DOWNLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_firmware_download)|下载固件映像的存储设备，但不进行激活。|
|[IOCTL_STORAGE_FIRMWARE_GET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_firmware_get_info)|查询详细的固件信息的存储设备。|
|[IOCTL_STORAGE_GET_DEVICE_NUMBER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_get_device_number)|返回**STORAGE_DEVICE_NUMBER**结构，其中包含 FILE_DEVICE_XXX 键入，number 的并且可分区的设备，设备启动时分配给设备驱动程序的分区号的设备。|
|[IOCTL_STORAGE_GET_HOTPLUG_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_get_hotplug_info)|检索指定的设备的热插拔配置。|
|[IOCTL_STORAGE_GET_LB_PROVISIONING_MAP_RESOURCES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_get_lb_provisioning_map_resources)|**IOCTL_STORAGE_GET_LB_PROVISIONING_MAP_RESOURCES**请求发送到的存储类驱动程序，以确定可用和已用的映射的存储设备上的资源。|
|[IOCTL_STORAGE_GET_MEDIA_SERIAL_NUMBER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_get_media_serial_number)|查询的 USB 设备序列号的 USB 泛型父驱动程序。|
|[IOCTL_STORAGE_GET_MEDIA_TYPES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_get_media_types)|返回有关该几何图形的软盘驱动器的信息。|
|[IOCTL_STORAGE_GET_MEDIA_TYPES_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_get_media_types_ex)|返回有关支持设备的媒体类型的信息。|
|[IOCTL_STORAGE_GET_PHYSICAL_ELEMENT_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_get_physical_element_status)|**IOCTL_STORAGE_GET_PHYSICAL_ELEMENT_STATUS**控制代码查询并返回从设备的物理元素状态。|
|[IOCTL_STORAGE_LOAD_MEDIA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_load_media)|会导致在调用方已打开的读取或写入访问的设备中加载的媒体。|
|[IOCTL_STORAGE_LOAD_MEDIA2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_load_media2)|会导致媒体以在调用方具有使用打开的设备中加载**FILE_READ_ATTRIBUTES**。|
|[IOCTL_STORAGE_MANAGE_DATA_SET_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_manage_data_set_attributes)|这**IOCTL_STORAGE_MANAGE_DATA_SET_ATTRIBUTES**请求用于将管理数据集属性请求发送到存储设备。|
|[IOCTL_STORAGE_MCN_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_mcn_control)|暂时启用或禁用即插即用的自定义事件传递**GUID_IO_MEDIA_ARRIVAL**并**GUID_IO_MEDIA_REMOVAL**可移动介质设备上。|
|[IOCTL_STORAGE_MEDIA_REMOVAL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_media_removal)|锁定设备，以防止删除媒体。|
|[IOCTL_STORAGE_PERSISTENT_RESERVE_IN](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_persistent_reserve_in)|通用存储类驱动程序 (classpnp.sys) 公开颁发中永久保留命令的 I/O 控制 (IOCTL) 接口。|
|[IOCTL_STORAGE_PERSISTENT_RESERVE_OUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_persistent_reserve_out)|通用存储类驱动程序 (classpnp.sys) 公开发出出永久保留命令的 I/O 控制 (IOCTL) 接口。|
|[IOCTL_STORAGE_PREDICT_FAILURE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_predict_failure)|轮询设备故障预测。|
|[IOCTL_STORAGE_PROTOCOL_COMMAND](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_protocol_command)|驱动程序可以使用**IOCTL_STORAGE_PROTOCOL_COMMAND**将特定于供应商的命令传递到存储设备|
|[IOCTL_STORAGE_QUERY_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_query_property)|驱动程序可以使用**IOCTL_STORAGE_QUERY_PROPERTY**返回存储设备或适配器的属性。|
|[IOCTL_STORAGE_READ_CAPACITY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_read_capacity)|**IOCTL_STORAGE_READ_CAPACITY**请求将返回目标存储设备的读取的容量信息。|
|[IOCTL_STORAGE_REINITIALIZE_MEDIA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_reinitialize_media)|驱动程序可以使用**IOCTL_STORAGE_REINITIALIZE_MEDIA**控制代码，以便重新初始化/擦除设备。|
|[IOCTL_STORAGE_RELEASE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_release)|释放用于支持多个发起程序的总线上调用方的独占使用和保留的设备，如 SCSI 总线的概念履行之前保留的设备。|
|[IOCTL_STORAGE_RESERVE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_reserve)|声明的设备上支持多个发起程序的总线调用方独占使用和保留的设备，如 SCSI 总线的概念。|
|[IOCTL_STORAGE_RESET_BUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_reset_bus)|重置的 I/O 总线和间接，总线上的每个设备。|
|[IOCTL_STORAGE_RESET_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_reset_device)|如果可能，请将非 SCSI 存储设备重置而不会影响在总线上的其他设备。|
|[IOCTL_STORAGE_SET_HOTPLUG_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_set_hotplug_info)|设置指定的设备的热插拔配置。|
|[IOCTL_STORAGE_SET_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_set_property)|指示是否成功的请求的属性进行更改，或将导致错误。
|[IOCTL_STORAGE_SET_TEMPERATURE_THRESHOLD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_set_temperature_threshold)|驱动程序可以使用**IOCTL_STORAGE_SET_TEMPERATURE_THRESHOLD**设置 （如果支持的硬件） 的存储设备的温度阈值。|