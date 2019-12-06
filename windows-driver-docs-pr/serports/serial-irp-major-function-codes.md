---
title: 串行 IRP 主要函数代码
description: 文档串行 IRP 主要功能代码
keywords:
- 串行设备 WDK
- 串行驱动程序 WDK
- 串行 IRP 代码
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2c6742c5c9e50dd212fce83387f6cb27c0451a0a
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "74862590"
---
# <a name="serial-irp-major-function-codes"></a>串行 IRP 主要函数代码
本主题介绍串行 IRP 主要功能代码。

标头： Wdm .h （包括 Wdm 或 Ntddk）

## <a name="irp_mj_create"></a>IRP_MJ_CREATE

[IRP_MJ_CREATE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)请求将打开一个串行设备。

### <a name="when-sent"></a>发送时间

客户端必须先打开串行设备，然后才能访问端口或连接到该端口的设备。

### <a name="input-parameters"></a>输入参数

无。

### <a name="output-parameters"></a>输出参数

无。

### <a name="io-status-block"></a>I/o 状态块

**信息**字段设置为零。

"**状态**" 字段设置为以下值之一：

|状态值|描述|
|----|----|
|STATUS_SUCCESS|已成功打开串行设备。|
|STATUS_ACCESS_DENIED|设备已打开。|
|STATUS_DELETE_PENDING|串行正在删除设备。|
|STATUS_INSUFFICIENT_RESOURCES|设备未处于即插即用启动状态，或驱动程序无法分配内部数据结构。|
|STATUS_NOT_A_DIRECTORY|串行设备无法作为目录打开。|
|STATUS_PENDING|序列排队等待以后处理请求。|
|STATUS_SHARED_IRQ_BUSY|分配给设备的中断正由其他打开的设备使用。|

### <a name="operation"></a>操作

必须先打开串行设备，然后才能使用该设备。 串行设备是一个专用设备;在任何给定时间，都只能打开一个端口上的一个文件。

## <a name="irp_mj_device_control"></a>IRP_MJ_DEVICE_CONTROL

IRP_MJ_DEVICE_CONTROL 请求将运行串行端口。

### <a name="when-sent"></a>发送时间

客户端使用设备控制请求来执行以下操作：

* 获取有关该端口的信息
* 获取并设置寄存器
* 获取和设置运行模式

有关串行支持的设备控制请求的说明，请参阅[ntddser](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/)标头。

### <a name="input-parameters"></a>输入参数

请求特定

### <a name="output-parameters"></a>输出参数

请求特定

### <a name="io-status-block"></a>I/o 状态块

请求特定

### <a name="operation"></a>操作

请求特定

## <a name="irp_mj_flush_buffers"></a>IRP_MJ_FLUSH_BUFFERS

[IRP_MJ_FLUSH_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)请求刷新串行设备的内部写入缓冲区。

### <a name="when-sent"></a>发送时间

客户端使用刷新请求来确定串行是否完成了客户端在刷新请求之前发送的所有写入请求。

### <a name="input-parameters"></a>输入参数

无。

### <a name="output-parameters"></a>输出参数

无。

### <a name="io-status-block"></a>I/o 状态块

**信息**成员设置为零。

**Status**成员设置为以下状态值之一：

|状态值|描述|
|----|----|
|STATUS_SUCCESS|请求已成功完成。|
|STATUS_CANCELLED|客户端已取消请求。 如果出现设备错误，则串行还会取消请求，并将串行配置为在出现设备错误时取消请求。|
|STATUS_DELETE_PENDING|驱动程序正在删除设备。|
|STATUS_PENDING|序列排队等待以后处理请求。|

### <a name="operation"></a>操作

串行队列，并按接收请求的顺序开始处理写入和刷新请求。 串行在为刷新请求之前收到的所有写入请求调用**IoCompleteRequest**后完成刷新请求。 *但是，完成刷新请求并不表示以前启动的所有写入请求均由设备堆栈中的其他驱动程序完成。* 例如，筛选器驱动程序可能仍在处理写入请求。 客户端必须检查设备堆栈中的所有驱动程序是否完成了写入请求，否则客户端将尝试释放或重新使用写入请求的 IRP。

## <a name="irp_mj_internal_device_control"></a>IRP_MJ_INTERNAL_DEVICE_CONTROL
[IRP_MJ_INTERNAL_DEVICE_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)请求在串行设备上设置内部运行模式。

### <a name="when-sent"></a>发送时间

客户端使用内部设备控制请求来执行以下操作：

* 获取并重置基本设置
* 控制等待/唤醒操作

有关内部设备控制请求的说明，请参阅[ntddser](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/)标头。

### <a name="input-parameters"></a>输入参数

请求特定

### <a name="output-parameters"></a>输出参数

请求特定

### <a name="io-status-block"></a>I/o 状态块

请求特定

### <a name="operation"></a>操作

请求特定

## <a name="irp_mj_pnp"></a>IRP_MJ_PNP

[IRP_MJ_PNP](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)请求支持即插即用。

### <a name="when-sent"></a>发送时间

PnP 管理器将 IRP_MJ_PNP 请求发送到查询设备以及启动、停止和删除设备。

### <a name="input-parameters"></a>输入参数

请求特定

### <a name="output-parameters"></a>输出参数

请求特定

### <a name="io-status-block"></a>I/o 状态块

请求特定

### <a name="operation"></a>操作

串行支持以下即插即用请求：

* [IRP_MN_CANCEL_REMOVE_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device)
* [IRP_MN_CANCEL_STOP_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-stop-device)
* [IRP_MN_FILTER_RESOURCE_REQUIREMENTS](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)
* [IRP_MN_QUERY_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)
* [IRP_MN_QUERY_DEVICE_RELATIONS](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)
* [IRP_MN_QUERY_ID](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)
* [IRP_MN_QUERY_PNP_DEVICE_STATE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-pnp-device-state)
* [IRP_MN_QUERY_REMOVE_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)
* [IRP_MN_QUERY_RESOURCE_REQUIREMENTS](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements)
* [IRP_MN_QUERY_STOP_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)
* [IRP_MN_REMOVE_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)
* [IRP_MN_START_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)
* [IRP_MN_STOP_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)
* [IRP_MN_SURPRISE_REMOVAL](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)

串行将所有其他即插即用请求关闭设备堆栈，无需进一步处理。

串行对即插即用请求执行以下特定于串行的处理：

**IRP_MN_QUERY_ID** （键入 BusQueryHardwardIDs）

如果串行设备在多端口 ISA 卡上，则串行会将宽字符 "* PNP0502" 追加到硬件 Id 字符串。

**IRP_MN_FILTER_RESOURCE_REQUIREMENTS**

多端口 ISA 卡上的串行设备共享相同的中断状态寄存器和相同的中断。

有关即插即用请求的一般操作的说明，请参阅[即插即用次要 irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps)。

## <a name="irp_mj_power"></a>IRP_MJ_POWER

[IRP_MJ_POWER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)请求控制电源管理。

### <a name="when-sent"></a>发送时间

Power manager 使用 power 请求来查询和设置电源状态。

###  <a name="input-parameters"></a>输入参数

请求特定

### <a name="output-parameters"></a>输出参数

请求特定

### <a name="io-status-block"></a>I/o 状态块

请求特定

### <a name="operation"></a>操作

串行支持以下电源请求：

* [IRP_MN_QUERY_POWER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)
* [IRP_MN_SET_POWER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)

串行按设备堆栈向下发送所有其他电源请求，由较低级别的驱动程序完成。

串行是串行设备堆栈的默认电源策略所有者，使用串行作为函数驱动程序或较低级别的筛选器驱动程序。

有关这些请求的一般操作的详细信息，请参阅[处理电源 irp 的规则](https://docs.microsoft.com/windows-hardware/drivers/kernel/rules-for-handling-power-irps)。

## <a name="irp_mj_query_information"></a>IRP_MJ_QUERY_INFORMATION

[IRP_MJ_QUERY_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-query-information)请求查询串行设备的文件结尾信息。 

### <a name="when-sent"></a>发送时间

客户端使用查询信息请求获取有关串行设备上打开的文件的标准信息和位置信息。

### <a name="input-parameters"></a>输入参数

**QueryFile. FileInformationClass**设置为**FileStandardInformation**或**FilePositionInformation**。

### <a name="output-parameters"></a>输出参数

|参数|描述|
|----|----|
|**FileStandardInformation**|**AssociatedIrp SystemBuffer**成员指向由串行用于输出标准信息的客户端分配 FILE_STANDARD_INFORMATION 结构。|
|**FilePositionInformation**|**AssociatedIrp SystemBuffer**成员指向客户端分配 FILE_POSITION_INFORMATION 结构，串行使用该结构来输出位置信息。|

### <a name="io-status-block"></a>I/o 状态块

如果请求成功，**信息**成员将设置为零。

**Status**成员设置为以下状态值之一：

|状态值|描述|
|----|----|
|STATUS_SUCCESS|请求已成功完成。|
|STATUS_CANCELLED|客户端已取消请求。 如果出现设备错误，则串行还会取消请求，并将串行配置为在出现设备错误时取消请求。|
|STATUS_DELETE_PENDING|串行正在删除设备。|
|STATUS_INVALID_PARAMETER|请求的信息不受支持。|
|STATUS_PENDING|序列排队等待以后处理请求。|

### <a name="operation"></a>操作

串行支持类型**FileStandardInformation**和**FilePositionInformation**的请求。

根据需要，标准文件信息始终设置为零或**FALSE**。 位置信息始终设置为零。

## <a name="irp_mj_read"></a>IRP_MJ_READ

[IRP_MJ_READ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)请求将数据从串行设备传输到客户端。

### <a name="when-sent"></a>发送时间

当客户端在串行设备上读取数据时使用读取请求。

### <a name="input-parameters"></a>输入参数

将. **Read. Length**成员设置为要传输到客户端的读取缓冲区的字节数。

### <a name="output-parameters"></a>输出参数

**AssociatedIrp SystemBuffer**成员指向客户端分配的读取缓冲区，串行在串行设备上读取数据。

### <a name="io-status-block"></a>I/o 状态块

**信息**成员设置为传输到客户端读取缓冲区的字节数。

**Status**成员设置为以下值之一：

|状态值|描述|
|----|----|
|STATUS_SUCCESS|请求已成功完成。|
|STATUS_CANCELLED|客户端已取消请求。 如果出现设备错误，则串行还会取消请求，并将串行配置为在出现设备错误时取消请求。|
|STATUS_DELETE_PENDING|串行正在删除设备。|
|STATUS_PENDING|序列排队等待以后处理请求。|
|STATUS_TIMEOUT|完成请求所用的时间超出了总超时值或间隔超时值。|

### <a name="operation"></a>操作

客户端可以使用超时事件来终止读取请求。 但请注意，当串行设备打开时，设备的超时设置不确定。 内核模式客户端可以使用[IOCTL_SERIAL_INTERNAL_BASIC_SETTINGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_internal_basic_settings)将超时参数设置为零（没有使用超时事件）。 用户模式和内核模式客户端可以使用[IOCTL_SERIAL_SET_TIMEOUTS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_timeouts)请求来设置超时参数。 

有关读写超时的详细信息，请参阅[设置串行设备的读取和写入超时](https://docs.microsoft.com/previous-versions/ff547486(v=vs.85))。

## <a name="irp_mj_set_information"></a>IRP_MJ_SET_INFORMATION

[IRP_MJ_SET_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)请求设置有关串行设备的文件结尾信息。

### <a name="when-sent"></a>发送时间

客户端使用 set information 请求更改在串行设备上打开的文件的当前文件尾位置。

### <a name="input-parameters"></a>输入参数
**SetFile. FileInformationClass**成员设置为**FileEndOfFileInformation**或**FileAllocationInformation**。

### <a name="output-parameters"></a>输出参数

无。

### <a name="io-status-block"></a>I/o 状态块

如果请求成功，**信息**成员将设置为零。

**Status**成员设置为以下状态值之一：

|状态值|描述|
|----|----|
|STATUS_SUCCESS|请求已成功完成。|
|STATUS_CANCELLED|客户端已取消请求。 如果出现设备错误，则串行还会取消请求，并将串行配置为在出现设备错误时取消请求。|
|STATUS_DELETE_PENDING|串行正在删除设备。|
|STATUS_INVALID_PARAMETER|不支持指定的文件结尾信息。|
|STATUS_PENDING|序列排队等待以后处理请求。|

### <a name="operation"></a>操作

串行支持类型**FileEndOfFileInformation**和**FileAllocationInformation**的请求。 但串行并不实际设置文件信息。 文件尾位置始终设置为零。

## <a name="irp_mj_system_control"></a>IRP_MJ_SYSTEM_CONTROL

[IRP_MJ_SYSTEM_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)请求支持 WMI 请求。

### <a name="when-sent"></a>发送时间

在串行注册为串行设备的 WMI 提供程序后，WMI 内核模式组件可随时发送 IRP_MJ_SYSTEM_CONTROL 请求。 通常在用户模式数据使用者请求 WMI 数据时发送 WMI Irp。

### <a name="input-parameters"></a>输入参数

请求特定

### <a name="output-parameters"></a>输出参数

请求特定

### <a name="io-status-block"></a>I/o 状态块

对于 WMI 请求，Serial 将状态字段设置为以下值之一：

|状态值|描述|
|----|----|
|STATUS_SUCCESS|请求已成功完成。|
|STATUS_BUFFER_TOO_SMALL|输出缓冲区的大小（以字节为单位）小于请求的信息所需的大小。|
|STATUS_INSUFFICIENT_RESOURCES|系统资源不足，无法保存串行端口名称。|
|STATUS_INVALID_DEVICE_REQUEST|请求无效。|
|STATUS_WMI_GUID_NOT_FOUND|不支持 WMI GUID。|

### <a name="operation"></a>操作

串行使用[WmiSystemControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 WMI 系统控制请求。 串行注册以下类型的 WMI 库回调例程， **WmiSystemControl**调用来处理发送到设备的 wmi 请求：

* [DpWmiQueryReginfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)
* [DpWmiQueryDataBlock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)
* [DpWmiSetDataBlock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_datablock_callback)
* [DpWmiSetDataItem](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_dataitem_callback)

串行不支持任何其他系统控制请求。 对于非 WMI 请求，Serial 会跳过当前堆栈位置，并沿设备堆栈向下发送请求。

串行注册下表中描述的 WMI GUID。

串行 WMI GUID 关联的数据结构 

| SERIAL_PORT_WMI_NAME_GUID | USHORT 后跟一个 WCSTR |
| ------------------------- | -------------------------- |
| SERIAL_PORT_WMI_COMM_GUID | SERIAL_WMI_COMM_DATA |
| SERIAL_PORT_WMI_HW_GUID | SERIAL_WMI_HW_DATA |
| SERIAL_PORT_WMI_PERF_GUID | SERIAL_WMI_PERF_DATA |
| SERIAL_PORT_WMI_PROPERTIES_GUID | WMI_SERIAL_PORT_PROPERTIES |

串行设备的 WMI 名称是设备的即插即用注册表项下的条目值**portvalue** 。

## <a name="irp_mj_write"></a>IRP_MJ_WRITE

[IRP_MJ_WRITE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)请求将数据从客户端传输到串行设备。

### <a name="when-sent"></a>发送时间

每当客户端向串行设备写入数据时都使用写入请求。

### <a name="input-parameters"></a>输入参数

将**Length**成员设置为要从客户端分配的写入缓冲区复制到串行设备的字节数。

**AssociatedIrp. SystemBuffer**成员指向客户端分配的写入缓冲区，串行从该缓冲区将数据复制到串行设备。

### <a name="output-parameters"></a>输出参数

无。

### <a name="io-status-block"></a>I/o 状态块

*信息*成员设置为实际从客户端的写入缓冲区复制到串行设备的字节数。

*Status*成员设置为以下值之一：

|状态值|描述|
|----|----|
|STATUS_SUCCESS|请求已成功完成。|
|STATUS_CANCELLED|客户端已取消请求。 如果出现设备错误，则串行还会取消请求，并将串行配置为在出现设备错误时取消请求。|
|STATUS_DELETE_PENDING|串行正在删除设备。|
|STATUS_PENDING|序列排队等待以后处理请求。|
|STATUS_TIMEOUT|超出写入请求允许的总时间。|

### <a name="operation"></a>操作

客户端可以使用超时事件终止写入请求。 但请注意，当串行设备打开时，在设备上设置的超时事件未定义。 内核模式客户端可以使用[IOCTL_SERIAL_INTERNAL_BASIC_SETTINGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_internal_basic_settings)将超时参数设置为零（没有使用超时事件）和[IOCTL_SERIAL_SET_TIMEOUTS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_timeouts)请求设置超时参数。 有关读写超时的详细信息，请参阅[设置串行设备的读取和写入超时](https://docs.microsoft.com/previous-versions/ff547486(v=vs.85))。

## <a name="related-topics"></a>相关主题

[即插即用次要 Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps)

[用于处理电源 Irp 的规则](https://docs.microsoft.com/windows-hardware/drivers/kernel/rules-for-handling-power-irps)

[串行控制器驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/serports/)
