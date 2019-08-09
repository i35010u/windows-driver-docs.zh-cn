---
title: 针对并行设备的 I/O 请求的特定于设备的操作
description: 记录并行设备 i/o 请求的设备特定操作
keywords:
- 并行设备 WDK
- 并行驱动程序 WDK
- 并行 IRP 代码
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3b4ed3ad500a19b9566aa52426e84984aa83fc12
ms.sourcegitcommit: d5f54510b9500413dd3084b59cb8869f2f6b13cf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "67376975"
---
# <a name="device-specific-operations-for-io-requests-for-parallel-devices"></a>针对并行设备的 I/O 请求的特定于设备的操作
本主题介绍针对并行设备 i/o 请求的下列特定于设备的操作

* [IRP_MJ_CREATE](#irp_mj_create)
* [IRP_MJ_DEVICE_CONTROL](#irp_mj_device_control)
* [IRP_MJ_INTERNAL_DEVICE_CONTROL](#irp_mj_internal_device_control)
* [IRP_MJ_QUERY_INFORMATION](#irp_mj_query_information)
* [IRP_MJ_READ](#irp_mj_read)
* [IRP_MJ_WRITE](#irp_mj_write)


##  <a name="irp_mj_create"></a>IRP_MJ_CREATE
[IRP_MJ_CREATE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)请求将打开一个并行设备。

### <a name="when-sent"></a>发送时间
客户端必须使用[IRP_MJ_CREATE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)请求打开并行设备, 然后才能访问设备。

### <a name="input-parameters"></a>输入参数
无。

### <a name="output-parameters"></a>输出参数
无。

### <a name="io-status-block"></a>I/O 状态块
信息成员设置为零。

Status 成员设置为以下值之一:


STATUS_SUCCESS 

设备已成功打开。

STATUS_ACCESS_DENIED 

设备已打开。

STATUS_DELETE_PENDING 

设备处于即插即用的删除状态。

STATUS_DEVICE_REMOVED 

设备已被删除。

STATUS_INVALID_DEVICE_REQUEST 

没有硬件。

STATUS_NOT_A_DIRECTORY 

设备不是目录。

### <a name="operation"></a>操作
并行设备是一个独占设备。 如果并行设备已打开, 则系统提供的针对并行端口的总线驱动程序会在设备关闭之前, 对该设备的所有后续[IRP_MJ_CREATE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)请求都将失败。 客户端必须在将其他 i/o 请求发送到设备之前打开并行设备, 或调用[并行设备回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

有关详细信息, 请参阅[打开和使用并行设备](https://docs.microsoft.com/windows-hardware/drivers/parports/opening-and-using-a-parallel-device)。


##  <a name="irp_mj_device_control"></a>IRP_MJ_DEVICE_CONTROL
[IRP_MJ_DEVICE_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求操作并行设备。

### <a name="when-sent"></a>发送时间
客户端对以下类型的操作使用设备控制请求:

* 获取有关设备的信息
* 设置设备的运行模式

请参阅[设备控制对并行设备的请求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

### <a name="input-parameters"></a>输入参数
请求特定的。

### <a name="output-parameters"></a>输出参数
请求特定的。

### <a name="io-status-block"></a>I/O 状态块
**信息**成员是请求特定的。 

**Status**成员设置为特定于请求的值, 或设置为以下一般状态值之一:


STATUS_SUCCESS
 
请求已成功完成。

STATUS_CANCELLED 

请求已取消。

STATUS_DELETE_PENDING 

正在删除该设备。

STATUS_DEVICE_REMOVED 

设备已被删除。

STATUS_INVALID_PARAMETER 

系统提供的并行端口总线驱动程序不支持该请求。

STATUS_PENDING 

请求处于挂起状态。

STATUS_UNSUCCESSFUL 

请求未成功完成。

### <a name="operation"></a>操作
操作是特定于请求的。


##  <a name="irp_mj_internal_device_control"></a>IRP_MJ_INTERNAL_DEVICE_CONTROL
[IRP_MJ_INTERNAL_DEVICE_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)请求在并行设备上设置内部运行模式。

### <a name="when-sent"></a>发送时间
客户端对以下类型的操作使用内部设备控制请求:

* 将并行端口的通信模式设置为与 IEEE 1284 兼容
* 获取有关并行端口的连接信息
* 锁定并解锁并行端口以供设备独占使用

请参阅[针对并行设备的内部设备控制请求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

### <a name="input-parameters"></a>输入参数
请求特定的。

### <a name="output-parameters"></a>输出参数
请求特定的。

### <a name="io-status-block"></a>I/O 状态块
**信息**成员是请求特定的。 

**Status**成员设置为特定于请求的值, 或设置为以下一般状态值之一:


STATUS_SUCCESS
 
请求已成功完成。

STATUS_CANCELLED 

请求已取消。

STATUS_DELETE_PENDING 

正在删除该设备。

STATUS_DEVICE_REMOVED 

设备已被删除。

STATUS_INVALID_PARAMETER 

并行总线驱动程序不支持该请求。

STATUS_PENDING 

请求处于挂起状态。

STATUS_UNSUCCESSFUL 

请求未成功完成。

### <a name="operation"></a>操作

操作是特定于请求的。


##  <a name="irp_mj_query_information"></a>IRP_MJ_QUERY_INFORMATION
[IRP_MJ_QUERY_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-query-information)请求获取有关代表并行设备的文件的信息。

### <a name="when-sent"></a>发送时间
客户端发送查询信息请求, 以确定文件指针的文件大小或当前字节偏移量。

### <a name="input-parameters"></a>输入参数
**QueryFile. FileInformationClass**成员设置为**FileStandardInformation**或**FilePositionInformation**。


**FileStandardInformation**请求:
 
**AssociatedIrp. SystemBuffer**成员指向一个[FILE_STANDARD_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_standard_information)结构, 客户端会将其分配给文件信息的输出。

**QueryFile**成员设置为**FILE_STANDARD_INFORMATION**结构的大小 (以字节为单位)。

**FilePositionInformation**请求: 

**AssociatedIrp. SystemBuffer**指向[FILE_POSITION_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_position_information)结构, 客户端将其分配给文件信息的输出。

**SetFile**成员设置为**FILE_POSITION_INFORMATION**结构的大小 (以字节为单位)。

### <a name="output-parameters"></a>输出参数
**AssociatedIrp. SystemBuffer**指向请求的信息。

**FileStandardInformation**请求类型: 

设置**FILE_STANDARD_INFORMATION**结构中的以下成员:

* **AllocationSize**设置为零。
* **EndOfFile**设置为**AllocationSize**成员的值。
* **NumberOfLinks**设置为零。
* **DeletePending**设置为**FALSE**。
* **Directory**设置为**FALSE**。

**FilePositionInformation**请求类型:
 
将**FILE_POSITION_INFORMATION**结构的**QuadPart**成员设置为零。

### <a name="io-status-block"></a>I/O 状态块
如果请求成功, 则将**信息**成员设置为与请求类型关联的结构的大小 (以字节为单位)。 否则,**信息**成员设置为零。

**Status**成员设置为以下状态值之一:


STATUS_SUCCESS 

请求已成功完成。

STATUS_BUFFER_TOO_SMALL 

由输入参数指定的结构的大小 (以字节为单位) 小于与请求类型关联的结构的大小 (以字节为单位)。

STATUS_DEVICE_REMOVED 

设备已被删除。

STATUS_INVALID_PARAMETER 

指定类型的信息无效。

### <a name="operation"></a>操作
系统提供的并行端口总线驱动程序支持查询以下类型的信息:

* **FileStandardInformation**
* **FilePositionInformation**


##  <a name="irp_mj_read"></a>IRP_MJ_READ
[IRP_MJ_READ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)请求从并行设备获取输入数据。

### <a name="when-sent"></a>发送时间
客户端使用[IRP_MJ_READ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)请求获取来自并行设备的输入。

### <a name="input-parameters"></a>输入参数
\- **Length**成员指向要从并行设备中读取的字节数。

### <a name="output-parameters"></a>输出参数
**AssociatedIrp SystemBuffer**成员指向客户端为读取数据分配的读取缓冲区。 缓冲区必须足够大才能容纳请求的字节数。

### <a name="io-status-block"></a>I/O 状态块
**信息**成员设置为实际从并行设备中读取的字节数。

**Status**成员设置为以下状态值之一:


STATUS_SUCCESS
 
请求已成功完成。

STATUS_DELETE_PENDING 

正在删除该设备。

STATUS_CANCELLED 

请求已取消。

STATUS_PENDING 

请求在并行设备的工作队列中排队。

STATUS_INVALID_PARAMETER 

**ByteOffset**成员不为零。 请注意, 读取和写入请求均使用此成员。

STATUS_DEVICE_REMOVED 

设备已被删除。

### <a name="operation"></a>操作
系统提供的并行端口总线驱动程序使用为并行设备设置的读取协议。 默认读取协议为 NIBBLE_MODE。 客户端可以使用[IOCTL_IEEE1284_NEGOTIATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_ieee1284_negotiate)请求来协商读取协议。

并行端口总线驱动程序为读取请求设置取消例程, 将读取请求标记为挂起, 并对工作队列上的读取请求进行排队。 读取请求保存在工作队列中, 该状态可在客户端完成或取消读取请求之前取消。

有关详细信息, 请参阅[读取和写入并行设备](https://docs.microsoft.com/windows-hardware/drivers/parports/reading-and-writing-a-parallel-device)。


##  <a name="irp_mj_write"></a>IRP_MJ_WRITE
[IRP_MJ_WRITE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)请求将输出数据传输到并行设备。

### <a name="when-sent"></a>发送时间
每当客户端将输出数据传输到并行设备时, 将使用[IRP_MJ_WRITE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)请求。

### <a name="input-parameters"></a>输入参数
**AssociatedIrp SystemBuffer**指向客户端为写入数据分配的写入缓冲区。 缓冲区必须足够大, 以容纳写入并行设备所需的字节数。

\- **Length**成员指向要写入到并行设备的字节数。

### <a name="output-parameters"></a>输出参数
无。

### <a name="io-status-block"></a>I/O 状态块
**信息**成员设置为实际写入到并行设备的字节数。

**Status**成员设置为以下值之一:

STATUS_SUCCESS
 
请求已成功完成。

STATUS_DELETE_PENDING 

正在删除该设备。

STATUS_CANCELLED 

请求已取消。

STATUS_PENDING 

请求在并行设备的工作队列中排队。

STATUS_INVALID_PARAMETER 

**ByteOffset**成员不为零。

STATUS_DEVICE_REMOVED 

设备已被删除。

### <a name="operation"></a>操作
系统提供的并行端口总线驱动程序通过使用为并行设备设置的写入协议传输数据。 默认写入协议为 CENTRONICS。 客户端可以使用[IOCTL_IEEE1284_NEGOTIATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_ieee1284_negotiate)请求来协商写入协议。 

并行端口总线驱动程序为写入请求设置取消例程, 将写入请求标记为 "挂起", 并在工作队列中对写入请求进行排队。 写入请求处于可取消状态, 直到完成或取消请求为止。

有关详细信息, 请参阅[读取和写入并行设备](https://docs.microsoft.com/windows-hardware/drivers/parports/reading-and-writing-a-parallel-device)。

## <a name="related-topics"></a>相关主题

[并行设备的设备控制请求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

[FILE_POSITION_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_position_information)[FILE_STANDARD_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_standard_information)

[打开和使用并行设备](https://docs.microsoft.com/windows-hardware/drivers/parports/opening-and-using-a-parallel-device)

[操作连接到并行端口的并行设备](https://docs.microsoft.com/windows-hardware/drivers/parports/operating-a-parallel-device-attached-to-a-parallel-port.md)

[并行设备回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[读取和写入并行设备](https://docs.microsoft.com/windows-hardware/drivers/parports/reading-and-writing-a-parallel-device)

