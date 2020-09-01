---
title: IRP_MJ_SHUTDOWN
description: 具有数据内部缓存的大容量存储设备的驱动程序必须在 DispatchShutdown 例程中处理此请求。
ms.date: 08/12/2017
ms.assetid: af0b01b5-5f81-42da-aa4b-433bd422a51f
keywords:
- IRP_MJ_SHUTDOWN 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 5bd06f97edfa026efcb33aaf512ab2dfd9dd67fe
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188245"
---
# <a name="irp_mj_shutdown"></a>IRP \_ MJ \_ 关闭


具有数据内部缓存的大容量存储设备的驱动程序必须在 [*DispatchShutdown*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中处理此请求。 如果基础驱动程序维护数据的内部缓冲区，则还必须处理此请求，同时分层的大容量存储设备和中间驱动程序的驱动程序也必须处理此请求。

<a name="when-sent"></a>发送时间
---------

接收到关闭请求指示正在发送文件系统驱动程序通知系统正在关闭。

当用户注销时，一个或多个文件系统驱动程序可以向此类低级驱动程序发送多个关闭请求，或者当系统出于其他原因而关闭时。

PnP 管理器以 IRQL 的形式发送此 IRP<= APC_LEVEL 在任意线程上下文中。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

<a name="operation"></a>操作
---------

驱动程序必须完成对设备中当前缓存的任何数据的传输，或在完成关闭请求之前保存在驱动程序的内部缓冲区中。

对于设备对象，驱动程序不会收到 **IRP \_ MJ \_ 关闭** 请求，除非它注册使用 [**IoRegisterShutdownNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregistershutdownnotification) 或 [**IoRegisterLastChanceShutdownNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterlastchanceshutdownnotification)来执行此操作。

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
<td>Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*DispatchShutdown*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[**IoRegisterLastChanceShutdownNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterlastchanceshutdownnotification)

[**IoRegisterShutdownNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregistershutdownnotification)

 

