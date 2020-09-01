---
title: 停止设备以重新平衡资源
description: 停止设备以重新平衡资源
ms.assetid: eed28d41-8a9d-4b9e-90d7-ea4ddeeaad2d
keywords:
- 重新平衡资源 WDK PnP
- 资源重新平衡 WDK PnP
- 暂停 PnP 设备
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e1d897b44b2ca0de05917bffd4650ec42277d1d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184741"
---
# <a name="stopping-a-device-to-rebalance-resources"></a>停止设备以重新平衡资源





下图显示了停止和重新启动设备以重新平衡资源所涉及的 Irp 的顺序。

![说明停止设备以重新平衡资源的示意图](images/stop-irps.png)

以下说明与上图中的带圆圈数字相对应：

1.  PnP 管理器会发出 [**IRP \_ MN \_ 查询 \_ 停止 \_ 设备**](./irp-mn-query-stop-device.md) ，询问设备的驱动程序是否可以停止设备并释放其硬件资源。

    如果设备堆栈中的所有驱动程序都返回状态 " \_ 成功"，则驱动程序会将设备置于状态 ("停止挂起") ，设备可以从该状态快速停止。

    PnP 管理器根据需要查询任意数量的设备堆栈以重新平衡所需的资源。

2.  PnP 管理器会发出 [**IRP \_ MN \_ 停止 \_ 设备**](./irp-mn-stop-device.md) ，停止设备。

    在 Windows 2000 和更高版本的 Windows 上，仅当已成功完成设备的以前的查询停止 IRP 时，PnP 管理器才会发送 "停止 IRP"。 为了响应停止 IRP，驱动程序会释放设备的硬件资源， (例如其 i/o 端口) 并保存需要访问设备的任何 Irp。

3.  成功重新平衡资源后，PnP 管理器会发出 [**IRP \_ MN \_ 启动 \_ 设备**](./irp-mn-start-device.md) 请求，重新启动重新平衡期间停止的任何设备。

4.  否则，PnP 管理器通过发送 [**IRP \_ MN \_ CANCEL \_ 停止 \_ 设备**](./irp-mn-cancel-stop-device.md)来取消查询停止 IRP。

    为了响应 **IRP \_ MN \_ CANCEL \_ 停止 \_ 设备**，设备的驱动程序会将设备恢复到 "已启动" 状态，并继续处理设备的 i/o 请求。

    如果堆栈中的一个驱动程序请求失败，或者如果总体重新平衡操作失败并且它取消了其所有的查询停止请求，则 PnP 管理器将取消设备堆栈的查询停止。 当 PnP 管理器只取消一个设备堆栈上的查询停止时，它将发送 **IRP \_ MN \_ CANCEL \_ 停止 \_ 设备** 请求，因为附加到该驱动程序的驱动程序上的任何驱动程序都使该设备处于停止挂起状态。 当 **IRP \_ MN \_ CANCEL \_ 停止 \_ 设备** 成功时，驱动程序已将设备恢复为 "已启动" 状态。

5.  如果重新平衡资源后，驱动程序无法重新启动设备，则 PnP 管理器会在 Windows 2000 和更高版本的 Windows) 上将删除 Irp 发送到设备堆栈 (。

    PnP 管理器首先发送 [**IRP \_ MN \_ 意外 \_ 删除**](./irp-mn-surprise-removal.md) 请求。 然后，它将发送 [**IRP \_ MN \_ REMOVE \_ 设备**](./irp-mn-remove-device.md) 请求，但只有在关闭了设备的所有打开句柄之后。

重新平衡 PnP 设备的硬件资源对应用程序和最终用户必须是透明的。 用户可能会遇到暂时的操作延迟，但数据不得丢失。 处理停止 Irp 时，必须考虑到这一点。

 

