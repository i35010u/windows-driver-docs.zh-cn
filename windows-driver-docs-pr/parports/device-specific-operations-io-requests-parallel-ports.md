---
title: 针对并行端口的 I/O 请求的特定于设备的操作
description: 文档的并行端口 I/O 请求的特定于设备的操作
keywords:
- WDK 的并行端口
- 并行驱动程序 WDK
- 并行 IRP 代码
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 38634b4c51f2009d3ca6ab7833a44296fa146248
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376959"
---
# <a name="device-specific-operations-for-io-requests-for-parallel-ports"></a>针对并行端口的 I/O 请求的特定于设备的操作
本主题介绍的并行端口 I/O 请求的以下特定于设备的操作：

* [IRP_MJ_CREATE](#irp_mj_create)
* [IRP_MJ_INTERNAL_DEVICE_CONTROL](#irp_mj_internal_device_control)


##  <a name="irpmjcreate"></a>IRP_MJ_CREATE 
[IRP_MJ_CREATE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)请求打开并行端口。

### <a name="when-sent"></a>发送时间
客户端必须使用[IRP_MJ_CREATE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)请求之前它可以访问的端口或设备打开并行端口连接到端口。

### <a name="input-parameters"></a>输入参数
无。

### <a name="output-parameters"></a>输出参数
无。

### <a name="io-status-block"></a>I/O 状态块
**信息**成员设置为零。

**状态**成员设置为以下值之一：


STATUS_SUCCESS
 
已成功打开并行端口。

STATUS_DELETE_PENDING 

设备是正插 manager 被删除。

### <a name="operation"></a>操作
并行端口是共享的设备。 当并行端口的系统提供的函数驱动程序收到了打开请求的并行端口时，它只是递增的并行端口上打开的文件的计数。


##   <a name="irpmjinternaldevicecontrol"></a>IRP_MJ_INTERNAL_DEVICE_CONTROL
[IRP_MJ_INTERNAL_DEVICE_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)请求并行端口上设置内部操作模式。

### <a name="when-sent"></a>发送时间
客户端发送内部设备控制请求以执行以下类型的操作：

* 获取有关该端口的信息
* 分配端口，或选择的端口上的设备
* 将通信模式设置

请参阅[内部设备控制请求的并行端口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

### <a name="input-parameters"></a>输入参数
输入是特定于请求的。

### <a name="output-parameters"></a>输出参数
输出是特定于请求的。

### <a name="io-status-block"></a>I/O 状态块
该信息成员是特定于请求的。 

状态成员设置为特定于请求的值或为以下泛型状态值之一：


STATUS_SUCCESS 

请求已成功完成。

STATUS_CANCELLED 

请求已取消。

STATUS_DELETE_PENDING 

驱动器是正被删除。

STATUS_INVALID_PARAMETER 

并行端口的系统提供的函数驱动程序不支持请求。

STATUS_PENDING 

请求处于挂起状态。

### <a name="operation"></a>操作
该操作是特定于请求的。

## <a name="related-topics"></a>相关主题

[内部设备控制请求的并行端口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[运行并行设备附加到并行端口](https://docs.microsoft.com/windows-hardware/drivers/parports/operating-a-parallel-device-attached-to-a-parallel-port.md)

