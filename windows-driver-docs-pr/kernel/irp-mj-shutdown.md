---
title: IRP_MJ_SHUTDOWN
description: 具有数据内部缓存的大容量存储设备的驱动程序必须在 DispatchShutdown 例程中处理此请求。
ms.date: 08/12/2017
ms.assetid: af0b01b5-5f81-42da-aa4b-433bd422a51f
keywords:
- IRP_MJ_SHUTDOWN 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: d5f6036e30fc3dbef2423e2a4e1b254a25e4ddbb
ms.sourcegitcommit: 5b0d2b7a3a4efa3bc4f94a769bf41d58d3321d50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72390723"
---
# <a name="irp_mj_shutdown"></a>IRP \_MJ \_SHUTDOWN


具有数据内部缓存的大容量存储设备的驱动程序必须在[*DispatchShutdown*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程中处理此请求。 如果基础驱动程序维护数据的内部缓冲区，则还必须处理此请求，同时分层的大容量存储设备和中间驱动程序的驱动程序也必须处理此请求。

<a name="when-sent"></a>发送时间
---------

接收到关闭请求指示正在发送文件系统驱动程序通知系统正在关闭。

当用户注销时，一个或多个文件系统驱动程序可以向此类低级驱动程序发送多个关闭请求，或者当系统出于其他原因而关闭时。

PnP 管理器以 IRQL < = APC_LEVEL 在任意线程上下文中发送此 IRP。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

<a name="operation"></a>操作
---------

驱动程序必须完成对设备中当前缓存的任何数据的传输，或在完成关闭请求之前保存在驱动程序的内部缓冲区中。

对于设备对象，驱动程序不会接收**IRP \_MJ \_SHUTDOWN**请求，除非它使用[**IoRegisterShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregistershutdownnotification)或[**IoRegisterLastChanceShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterlastchanceshutdownnotification)注册来执行此操作。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wdm .h （包括 Wdm、Ntddk 或 Ntifs）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*DispatchShutdown*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[**IoRegisterLastChanceShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterlastchanceshutdownnotification)

[**IoRegisterShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregistershutdownnotification)

 

 




