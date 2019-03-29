---
title: 停止设备以将其禁用 (Windows 98/Me)
description: 停止设备以将其禁用 (Windows 98/Me)
ms.assetid: 2fc42fe4-ad29-4a51-9560-74b568bcd129
keywords:
- 禁用即插即用设备
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 082ebff5e3412fa32311522501e1d0bcebec2c65
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563137"
---
# <a name="stopping-a-device-to-disable-it-windows-98me"></a>停止设备以将其禁用 (Windows 98/Me)





在 Windows 98 上 / 我，即插即用 manager 问题 Irp 时停止设备管理器禁用的设备。 (Windows 2000 和更高版本的 Windows 问题[删除 Irp](removing-a-device.md)在此情况下)。

PnP 管理器将停止 Irp 发送按以下顺序：

1.  即插即用 manager 问题[ **IRP\_MN\_查询\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551725)要求设备的驱动程序是否可以停用设备。

    如果设备堆栈中的所有驱动程序返回状态\_成功后，驱动程序已将设备置于 （停止挂起） 的状态从该设备可以快速停止。

    PnP 管理器查询根据需要禁用该设备的任意多个设备堆栈。

2.  如果**IRP\_MN\_查询\_停止\_设备**成功，即插即用 manager 问题[ **IRP\_MN\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551755)停用设备。

    PnP 管理器将发送停止 IRP，仅当设备上一个查询停止 IRP 已成功完成。 在响应停止 IRP，驱动程序释放设备的硬件资源 （如其 I/O 端口） 和失败要求设备的访问权限的任何 Irp。

3.  如果**IRP\_MN\_查询\_停止\_设备**失败，即插即用管理器将发送[ **IRP\_MN\_取消\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff550826)取消查询。

    以响应**IRP\_MN\_取消\_停止\_设备**，设备的驱动程序将设备恢复为已启动状态并继续处理 I/O 请求的设备。

    如果堆栈中的一个驱动程序失败的请求，即插即用管理器取消设备堆栈查询停止。 当 PnP 管理器取消只是一个设备堆栈上的查询停止时，它会发送**IRP\_MN\_取消\_停止\_设备**请求，因为上面驱动程序连接的任何驱动程序失败查询中的停止挂起状态持有该设备。 当**IRP\_MN\_取消\_停止\_设备**成功，驱动程序返回了错误的设备已启动状态。

禁用设备后，其驱动程序无法排队传入 Irp，因为保证时可能会重新启用该设备。 因此，可能会丢失数据。

 

 




