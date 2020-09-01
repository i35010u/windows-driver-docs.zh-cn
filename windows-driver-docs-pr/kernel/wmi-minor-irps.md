---
title: WMI 次要 IRP
description: WMI 次要 IRP
ms.date: 08/12/2017
ms.assetid: 5788294f-2145-4381-9b06-3b138b2d26df
ms.localizationpriority: medium
ms.openlocfilehash: d998ab77e905138e15ba83c6a32862a3b205b8c2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190021"
---
# <a name="wmi-minor-irps"></a>WMI 次要 IRP





本部分介绍作为 WDM 的 WMI 扩展的一部分的 [Windows Management Instrumentation](./implementing-wmi.md) irp。 所有 WMI Irp 均使用主要代码 [**IRP \_ MJ \_ 系统 \_ 控件**](irp-mj-system-control.md) 和指示特定 WMI 请求的次要代码。 在将驱动程序的成功注册作为 WMI 数据的供应商后，WMI 内核模式组件就可以随时发送 WMI Irp。 WMI Irp 通常在用户模式数据使用者请求 WMI 数据时发送。

所有驱动程序都必须设置调度表入口点， [*DispatchSystemControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程才能处理 WMI 请求。

如果驱动程序通过调用 [**IoWMIRegistrationControl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)注册为 wmi 数据提供程序，则必须使用 [处理 wmi 请求](./handling-wmi-requests.md)中所述的一种方法来处理 wmi irp。

未注册为 WMI 数据提供程序的驱动程序必须将所有 WMI 请求转发到下一个较低的驱动程序。

本部分介绍以下系统定义的 WMI 次要函数代码：

[**IRP \_ MN \_ 更改 \_ 单一 \_ 实例**](irp-mn-change-single-instance.md)

[**IRP \_ MN \_ 更改 \_ 单个 \_ 项目**](irp-mn-change-single-item.md)

[**IRP \_ MN \_ 禁用 \_ 收集**](irp-mn-disable-collection.md)

[**IRP \_ MN \_ 禁用 \_ 事件**](irp-mn-disable-events.md)

[**IRP \_ MN \_ 启用 \_ 收集**](irp-mn-enable-collection.md)

[**IRP \_ MN \_ 启用 \_ 事件**](irp-mn-enable-events.md)

[**IRP \_ MN \_ EXECUTE \_ 方法**](irp-mn-execute-method.md)

[**IRP \_ MN \_ 查询 \_ 所有 \_ 数据**](irp-mn-query-all-data.md)

[**IRP \_ MN \_ 查询 \_ 单一 \_ 实例**](irp-mn-query-single-instance.md)

[**IRP \_ MN \_ REGINFO**](irp-mn-reginfo.md)

[**IRP \_ MN \_ REGINFO \_ EX**](irp-mn-reginfo-ex.md)

如果驱动程序收到一个 IRP，其中包含任何其他 IRP 次要函数代码，则应将 IRP 转发到下一个较低版本的驱动程序。

 

