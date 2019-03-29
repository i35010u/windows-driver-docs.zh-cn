---
title: 针对并行设备的 I/O 请求的特定于设备的操作
description: 文档的并行设备的 I/O 请求的特定于设备的操作
keywords:
- 并行设备 WDK
- 并行驱动程序 WDK
- 并行 IRP 代码
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 39f253f9095a330932c22673dc9b2f2528d618c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565502"
---
# <a name="device-specific-operations-for-io-requests-for-parallel-devices"></a>针对并行设备的 I/O 请求的特定于设备的操作
本主题介绍并行设备的 I/O 请求的以下特定于设备的操作

* [IRP_MJ_CREATE](#irp_mj_create)
* [IRP_MJ_DEVICE_CONTROL](#irp_mj_device_control)
* [IRP_MJ_INTERNAL_DEVICE_CONTROL](#irp_mj_internal_device_control)
* [IRP_MJ_QUERY_INFORMATION](#irp_mj_query_information)
* [IRP_MJ_READ](#irp_mj_read)
* [IRP_MJ_WRITE](#irp_mj_write)


##  <a name="irpmjcreate"></a>IRP_MJ_CREATE
[IRP_MJ_CREATE](https://msdn.microsoft.com/library/windows/hardware/ff550729)请求打开并行设备。

### <a name="when-sent"></a>发送时间
客户端必须使用[IRP_MJ_CREATE](https://msdn.microsoft.com/library/windows/hardware/ff550729)请求打开并行设备才能访问设备。

### <a name="input-parameters"></a>输入参数
无。

### <a name="output-parameters"></a>输出参数
无。

### <a name="io-status-block"></a>I/O 状态块
信息成员设置为零。

状态成员设置为以下值之一：


STATUS_SUCCESS 

设备已成功打开。

STATUS_ACCESS_DENIED 

设备已打开。

STATUS_DELETE_PENDING 

设备处于插很吃惊，删除状态。

STATUS_DEVICE_REMOVED 

已删除设备。

STATUS_INVALID_DEVICE_REQUEST 

没有存在硬件。

STATUS_NOT_A_DIRECTORY 

设备不是一个目录。

### <a name="operation"></a>操作
并行设备是独占的设备。 如果并行设备处于打开状态，并行端口的系统提供的总线驱动程序失败，任何后续[IRP_MJ_CREATE](https://msdn.microsoft.com/library/windows/hardware/ff550729)设备在关闭设备之前的请求。 其他输入/输出请求发送到设备或调用之前，必须打开并行设备客户端[并行设备回调例程](https://msdn.microsoft.com/library/windows/hardware/ff544275)。

有关详细信息，请参阅[打开并使用并行设备](https://msdn.microsoft.com/windows/hardware/drivers/parports/opening-and-using-a-parallel-device)。


##  <a name="irpmjdevicecontrol"></a>IRP_MJ_DEVICE_CONTROL
[IRP_MJ_DEVICE_CONTROL](https://msdn.microsoft.com/library/windows/hardware/ff550744)请求运行并行设备。

### <a name="when-sent"></a>发送时间
客户端对以下类型的操作使用设备控制请求：

* 获取有关设备的信息
* 设置设备的运行模式

请参阅[并行的设备的设备控制请求](https://msdn.microsoft.com/library/windows/hardware/ff543945)。

### <a name="input-parameters"></a>输入参数
特定于请求的。

### <a name="output-parameters"></a>输出参数
特定于请求的。

### <a name="io-status-block"></a>I/O 状态块
**信息**成员是特定于请求的。 

**状态**成员设置为特定于请求的值或为以下泛型状态值之一：


STATUS_SUCCESS
 
请求已成功完成。

STATUS_CANCELLED 

请求已取消。

STATUS_DELETE_PENDING 

设备是正被删除。

STATUS_DEVICE_REMOVED 

已删除设备。

STATUS_INVALID_PARAMETER 

并行端口的系统提供的总线驱动程序不支持请求。

STATUS_PENDING 

请求处于挂起状态。

STATUS_UNSUCCESSFUL 

请求未成功完成。

### <a name="operation"></a>操作
该操作是特定于请求的。


##  <a name="irpmjinternaldevicecontrol"></a>IRP_MJ_INTERNAL_DEVICE_CONTROL
[IRP_MJ_INTERNAL_DEVICE_CONTROL](https://msdn.microsoft.com/library/windows/hardware/ff550766)请求设置并行的设备上的内部操作模式。

### <a name="when-sent"></a>发送时间
客户端对以下类型的操作使用内部设备控制请求：

* 将并行端口的通信模式设置为 IEEE 1284 兼容
* 获取有关并行端口的连接信息
* 锁定和解锁独占使用的并行端口设备

请参阅内部[并行的设备的设备控制请求](https://msdn.microsoft.com/library/windows/hardware/ff543945)。

### <a name="input-parameters"></a>输入参数
特定于请求的。

### <a name="output-parameters"></a>输出参数
特定于请求的。

### <a name="io-status-block"></a>I/O 状态块
**信息**成员是特定于请求的。 

**状态**成员设置为特定于请求的值或为以下泛型状态值之一：


STATUS_SUCCESS
 
请求已成功完成。

STATUS_CANCELLED 

请求已取消。

STATUS_DELETE_PENDING 

设备是正被删除。

STATUS_DEVICE_REMOVED 

已删除设备。

STATUS_INVALID_PARAMETER 

并行总线驱动程序不支持请求。

STATUS_PENDING 

请求处于挂起状态。

STATUS_UNSUCCESSFUL 

请求未成功完成。

### <a name="operation"></a>操作

该操作是特定于请求的。


##  <a name="irpmjqueryinformation"></a>IRP_MJ_QUERY_INFORMATION
[IRP_MJ_QUERY_INFORMATION](https://msdn.microsoft.com/library/windows/hardware/ff550788)请求获取有关文件表示并行设备的信息。

### <a name="when-sent"></a>发送时间
客户端发送查询信息请求，以确定文件大小或文件指针的当前字节偏移量。

### <a name="input-parameters"></a>输入参数
**Parameters.QueryFile.FileInformationClass**成员设置为**FileStandardInformation**或**FilePositionInformation**。


**FileStandardInformation**请求：
 
**AssociatedIrp.SystemBuffer**成员将指向[FILE_STANDARD_INFORMATION](https://msdn.microsoft.com/library/windows/hardware/ff545855)为输出的文件信息的客户端分配的结构。

**Parameters.QueryFile.Length**的成员设置为的大小，以字节为单位， **FILE_STANDARD_INFORMATION**结构。

**FilePositionInformation**请求： 

**AssociatedIrp.SystemBuffer**指向[FILE_POSITION_INFORMATION](https://msdn.microsoft.com/library/windows/hardware/ff545848)为输出的文件信息的客户端分配的结构。

**Parameters.SetFile.Length**的成员设置为的大小，以字节为单位， **FILE_POSITION_INFORMATION**结构。

### <a name="output-parameters"></a>输出参数
**AssociatedIrp.SystemBuffer**指向所请求的信息。

**FileStandardInformation**请求类型： 

设置中的以下成员**FILE_STANDARD_INFORMATION**结构：

* **AllocationSize.QuadPart**设置为零。
* **EndOfFile**设置为值**AllocationSize**成员。
* **NumberOfLinks**设置为零。
* **DeletePending**设置为**FALSE**。
* **目录**设置为**FALSE**。

**FilePositionInformation**请求类型：
 
集**CurrentByteOffset.QuadPart**的成员**FILE_POSITION_INFORMATION**为零的结构。

### <a name="io-status-block"></a>I/O 状态块
如果请求成功，**信息**成员设置为大小 （字节） 与请求的类型相关联的结构。 否则为**信息**成员设置为零。

**状态**成员设置为以下状态的值之一：


STATUS_SUCCESS 

请求已成功完成。

STATUS_BUFFER_TOO_SMALL 

大小 （字节） 结构，通过输入参数，指定小于大小 （字节） 与请求类型相关联的结构。

STATUS_DEVICE_REMOVED 

已删除设备。

STATUS_INVALID_PARAMETER 

指定的类型不是信息的有效的。

### <a name="operation"></a>操作
并行端口的系统提供的总线驱动程序支持以下类型的信息的查询：

* **FileStandardInformation**
* **FilePositionInformation**


##  <a name="irpmjread"></a>IRP_MJ_READ
[IRP_MJ_READ](https://msdn.microsoft.com/library/windows/hardware/ff550794)请求从并行设备获取输入的数据。

### <a name="when-sent"></a>发送时间
客户端用[IRP_MJ_READ](https://msdn.microsoft.com/library/windows/hardware/ff550794)请求以获取从并行设备的输入。

### <a name="input-parameters"></a>输入参数
**Parameters.Read.Length**成员指向要从并行设备读取的字节数。

### <a name="output-parameters"></a>输出参数
**AssociatedIrp.SystemBuffer**成员指向为读取数据的客户端分配的读取缓冲区。 缓冲区必须足够大以保存请求的字节数。

### <a name="io-status-block"></a>I/O 状态块
**信息**成员设置为从并行设备中实际读取的字节数。

**状态**成员设置为以下状态的值之一：


STATUS_SUCCESS
 
请求已成功完成。

STATUS_DELETE_PENDING 

设备是正被删除。

STATUS_CANCELLED 

请求已取消。

STATUS_PENDING 

请求是在并行设备的工作队列中排队。

STATUS_INVALID_PARAMETER 

**Parameters.Write.ByteOffset**成员不为零。 请注意，读和写请求使用此成员。

STATUS_DEVICE_REMOVED 

已删除设备。

### <a name="operation"></a>操作
并行端口的系统提供的总线驱动程序使用读取的协议为并行设备设置。 默认值读取协议是 NIBBLE_MODE。 客户端可以通过使用协商读取的协议[IOCTL_IEEE1284_NEGOTIATE](https://msdn.microsoft.com/library/windows/hardware/ff543978)请求。

并行端口总线驱动程序设置在取消例程的读取请求、 将标记为挂起，则读取的请求和队列上的工作队列的读取的请求。 读取的请求会保留在工作队列中可以取消，直到完成或取消由客户端读取的请求的状态。

有关详细信息，请参阅[读取和写入并行设备](https://msdn.microsoft.com/windows/hardware/drivers/parports/reading-and-writing-a-parallel-device)。


##  <a name="irpmjwrite"></a>IRP_MJ_WRITE
[IRP_MJ_WRITE](https://msdn.microsoft.com/library/windows/hardware/ff550819)请求将输出数据传输到并行的设备。

### <a name="when-sent"></a>发送时间
客户端用[IRP_MJ_WRITE](https://msdn.microsoft.com/library/windows/hardware/ff550819)请求时它将输出数据传输到并行的设备。

### <a name="input-parameters"></a>输入参数
**AssociatedIrp.SystemBuffer**指向客户端分配的写入缓冲区写入数据。 缓冲区必须足够大以保存请求的字节写入到并行的设备数。

**Parameters.Write.Length**成员指向要写入到并行的设备的字节数。

### <a name="output-parameters"></a>输出参数
无。

### <a name="io-status-block"></a>I/O 状态块
**信息**成员设置为实际写入到并行的设备的字节数。

**状态**成员设置为以下值之一：

STATUS_SUCCESS
 
请求已成功完成。

STATUS_DELETE_PENDING 

设备是正被删除。

STATUS_CANCELLED 

请求已取消。

STATUS_PENDING 

请求是在并行设备的工作队列中排队。

STATUS_INVALID_PARAMETER 

**Parameters.Write.ByteOffset**成员不为零。

STATUS_DEVICE_REMOVED 

已删除设备。

### <a name="operation"></a>操作
并行端口的系统提供的总线驱动程序将通过使用并行设备设置写入协议传输数据。 默认写入协议为 CENTRONICS。 客户端可以通过使用协商写协议[IOCTL_IEEE1284_NEGOTIATE](https://msdn.microsoft.com/library/windows/hardware/ff543978)请求。 

并行端口总线驱动程序设置写入请求的取消例程，将标记为挂起，写入请求和队列工作队列中的写入请求。 写入请求都保存在可以取消，直到完成或取消请求的状态。

有关详细信息，请参阅[读取和写入并行设备](https://msdn.microsoft.com/windows/hardware/drivers/parports/reading-and-writing-a-parallel-device)。

## <a name="related-topics"></a>相关主题

[适用于并行设备的设备控制请求](https://msdn.microsoft.com/library/windows/hardware/ff543945)。

[FILE_POSITION_INFORMATION](https://msdn.microsoft.com/library/windows/hardware/ff545848) [FILE_STANDARD_INFORMATION](https://msdn.microsoft.com/library/windows/hardware/ff545855)

[打开并使用并行设备](https://msdn.microsoft.com/windows/hardware/drivers/parports/opening-and-using-a-parallel-device)

[运行并行设备附加到并行端口](https://msdn.microsoft.com/windows/hardware/drivers/parports/operating-a-parallel-device-attached-to-a-parallel-port.md)

[并行设备回调例程](https://msdn.microsoft.com/library/windows/hardware/ff544275)

[读取和写入并行设备](https://msdn.microsoft.com/windows/hardware/drivers/parports/reading-and-writing-a-parallel-device)

