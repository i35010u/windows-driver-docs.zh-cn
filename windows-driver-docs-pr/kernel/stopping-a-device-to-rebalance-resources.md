---
title: 停止设备以重新平衡资源
description: 停止设备以重新平衡资源
ms.assetid: eed28d41-8a9d-4b9e-90d7-ea4ddeeaad2d
keywords:
- 重新平衡资源 WDK 即插即用
- 重新平衡即插即用的 WDK 资源
- 正在暂停的即插即用设备
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5dd80d3981f3f7bece37a14f35ae8f4b100ad61
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382980"
---
# <a name="stopping-a-device-to-rebalance-resources"></a>停止设备以重新平衡资源





下图显示 Irp 的序列所涉及到停止并重新启动设备来重新平衡资源。

![说明停止设备来重新平衡资源的关系图](images/stop-irps.png)

以下说明与上图中带圆圈的数字相对应：

1.  即插即用 manager 问题[ **IRP\_MN\_查询\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)要求设备的驱动程序是否可以停止设备和发布其硬件资源。

    如果设备堆栈中的所有驱动程序返回状态\_成功后，驱动程序已将设备置于 （停止挂起） 的状态从该设备可以快速停止。

    PnP 管理器根据需要重新平衡所需的资源查询多设备堆栈。

2.  即插即用 manager 问题[ **IRP\_MN\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)停用设备。

    在 Windows 2000 和更高版本的 Windows，即插即用管理器发送停止 IRP，仅当设备已成功完成上一个查询停止 IRP。 响应停止 IRP，驱动程序版本设备的硬件资源 （例如其 I/O 端口） 和保存任何需要访问设备的 Irp。

3.  已成功重新平衡资源之后, 即插即用的管理器将发出[ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求重新启动它停止在任何设备重新平衡。

4.  否则，即插即用管理器将通过发送取消查询停止 IRP [ **IRP\_MN\_取消\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-stop-device)。

    以响应**IRP\_MN\_取消\_停止\_设备**，设备的驱动程序将设备恢复为已启动状态并继续处理 I/O 请求的设备。

    PnP 管理器取消设备堆栈查询停止，如果在堆栈中的一个驱动程序失败的请求或如果整体重新平衡操作失败，并且它正在取消所有其查询停止请求。 当 PnP 管理器取消只是一个设备堆栈上的查询停止时，它会发送**IRP\_MN\_取消\_停止\_设备**请求，因为上面驱动程序连接的任何驱动程序失败查询中的停止挂起状态持有该设备。 当**IRP\_MN\_取消\_停止\_设备**成功，驱动程序返回了错误的设备已启动状态。

5.  如果驱动程序无法重新均衡资源后，重启设备，即插即用的管理器发送到设备堆栈 （在 Windows 2000 和更高版本的 Windows） 删除 Irp。

    PnP 管理器第一次发送[ **IRP\_MN\_惊讶\_删除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)请求。 然后它将发送[ **IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)关闭请求，但仅当所有打开句柄设备。

重新平衡即插即用设备的硬件资源必须是对应用程序和最终用户透明。 用户可能会遇到暂时的延迟在操作中，但数据不会丢失。 必须考虑到这一点在处理时停止进行 Irp。

 

 




