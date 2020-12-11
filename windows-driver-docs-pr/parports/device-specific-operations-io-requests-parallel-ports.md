---
title: 针对并行端口的 I/O 请求的特定于设备的操作
description: 记录并行端口 i/o 请求的设备特定操作
keywords:
- 并行端口 WDK
- 并行驱动程序 WDK
- 并行 IRP 代码
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fa6293aed837c98445dba6114153bacfa8d7d680
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091002"
---
# <a name="device-specific-operations-for-io-requests-for-parallel-ports"></a>针对并行端口的 I/O 请求的特定于设备的操作
本主题介绍针对并行端口 i/o 请求的下列特定于设备的操作：

* [IRP_MJ_CREATE](#irp_mj_create)
* [IRP_MJ_INTERNAL_DEVICE_CONTROL](#irp_mj_internal_device_control)


## <a name="irp_mj_create"></a><a name="irp_mj_create"></a> IRP_MJ_CREATE
[IRP_MJ_CREATE](../kernel/irp-mj-create.md)请求将打开一个并行端口。

### <a name="when-sent"></a>发送时间
客户端必须使用 [IRP_MJ_CREATE](../kernel/irp-mj-create.md) 请求来打开并行端口，然后才能访问端口或连接到该端口的设备。

### <a name="input-parameters"></a>输入参数
无。

### <a name="output-parameters"></a>输出参数
无。

### <a name="io-status-block"></a>I/o 状态块
**信息** 成员设置为零。

**Status** 成员设置为以下值之一：


STATUS_SUCCESS
 
已成功打开并行端口。

STATUS_DELETE_PENDING 

设备正在被即插即用管理器删除。

### <a name="operation"></a>操作
并行端口是共享设备。 系统提供的并行端口函数驱动程序收到并行端口的打开请求时，只需递增并行端口上打开文件的计数。


## <a name="irp_mj_internal_device_control"></a><a name="irp_mj_internal_device_control"></a> IRP_MJ_INTERNAL_DEVICE_CONTROL
[IRP_MJ_INTERNAL_DEVICE_CONTROL](../kernel/irp-mj-internal-device-control.md)请求在并行端口上设置内部运行模式。

### <a name="when-sent"></a>发送时间
客户端发送内部设备控制请求来执行以下类型的操作：

* 获取有关该端口的信息
* 分配端口或选择端口上的设备
* 设置通信模式

请参阅 [内部设备控制并行端口请求](/windows-hardware/drivers/ddi/parallel)。

### <a name="input-parameters"></a>输入参数
输入是请求特定的。

### <a name="output-parameters"></a>输出参数
输出是请求特定的。

### <a name="io-status-block"></a>I/o 状态块
信息成员是请求特定的。 

Status 成员设置为特定于请求的值，或设置为以下常规状态值之一：


STATUS_SUCCESS 

请求已成功完成。

STATUS_CANCELLED 

请求已被取消。

STATUS_DELETE_PENDING 

正在删除驱动器。

STATUS_INVALID_PARAMETER 

系统提供的并行端口函数驱动程序不支持该请求。

STATUS_PENDING 

请求处于挂起状态。

### <a name="operation"></a>操作
操作是特定于请求的。

## <a name="related-topics"></a>相关主题

[并行端口的内部设备控制请求](/windows-hardware/drivers/ddi/parallel)

[打开连接到并行端口的并行设备](./operating-a-parallel-device-attached-to-a-parallel-port.md)