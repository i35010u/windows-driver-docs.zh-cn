---
title: 停止设备以将其禁用 (Windows 98/Me)
description: 停止设备以将其禁用 (Windows 98/Me)
ms.assetid: 2fc42fe4-ad29-4a51-9560-74b568bcd129
keywords:
- 禁用 PnP 设备
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ded6e2fb17a07671e04e20d445c8a628e1a67213
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184735"
---
# <a name="stopping-a-device-to-disable-it-windows-98me"></a>停止设备以将其禁用 (Windows 98/Me)





在 Windows 98/Me 上，当设备管理器禁用设备时，PnP 管理器会发出停止 Irp。 Windows 2000 和更高版本的 Windows (在这种情况下 [删除 irp](removing-a-device.md)) 。

PnP 管理器按以下顺序发送停止 Irp：

1.  PnP 管理器发出 [**IRP \_ MN \_ 查询 \_ 停止 \_ 设备**](./irp-mn-query-stop-device.md) ，询问设备的驱动程序是否可以停止该设备。

    如果设备堆栈中的所有驱动程序都返回状态 " \_ 成功"，则驱动程序会将设备置于状态 ("停止挂起") ，设备可以从该状态快速停止。

    PnP 管理器根据需要查询任意数量的设备堆栈，以禁用该设备。

2.  如果 **irp \_ MN \_ 查询 \_ 停止 \_ 设备** 成功，PnP 管理器会发出 [**IRP \_ MN \_ 停止 \_ 设备**](./irp-mn-stop-device.md) 以停止设备。

    仅当已成功完成设备的前一个查询停止 IRP 时，PnP 管理器才会发送 "停止 IRP"。 为了响应停止 IRP，驱动程序会释放设备的硬件资源 (如其 i/o 端口) 并导致需要访问该设备的任何 Irp 失败。

3.  如果 **IRP \_ MN \_ 查询 \_ 停止 \_ 设备** 失败，PnP 管理器将发送 [**IRP \_ MN \_ 取消 \_ 停止 \_ 设备**](./irp-mn-cancel-stop-device.md) 以取消查询。

    为了响应 **IRP \_ MN \_ CANCEL \_ 停止 \_ 设备**，设备的驱动程序会将设备恢复到 "已启动" 状态，并继续处理设备的 i/o 请求。

    如果堆栈中的一个驱动程序未能请求，PnP 管理器将取消设备堆栈的查询停止。 当 PnP 管理器只取消一个设备堆栈上的查询停止时，它将发送 **IRP \_ MN \_ CANCEL \_ 停止 \_ 设备** 请求，因为附加到该驱动程序的驱动程序上的任何驱动程序都使该设备处于停止挂起状态。 当 **IRP \_ MN \_ CANCEL \_ 停止 \_ 设备** 成功时，驱动程序已将设备恢复为 "已启动" 状态。

如果设备处于禁用状态，则其驱动程序无法将传入的 Irp 排队，因为无法保证设备的重新启用。 因此，数据可能会丢失。

 

