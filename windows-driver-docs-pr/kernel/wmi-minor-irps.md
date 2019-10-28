---
title: WMI 次要 IRP
description: WMI 次要 IRP
ms.date: 08/12/2017
ms.assetid: 5788294f-2145-4381-9b06-3b138b2d26df
ms.localizationpriority: medium
ms.openlocfilehash: abe1f2e0dd4c93a96e204c81b44662afb9876539
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838304"
---
# <a name="wmi-minor-irps"></a>WMI 次要 IRP





本部分介绍作为 WDM 的 WMI 扩展的一部分的[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi) irp。 所有 WMI Irp 均使用主要的代码[**IRP\_MJ\_系统\_控件**](irp-mj-system-control.md)和指示特定 WMI 请求的次要代码。 在将驱动程序的成功注册作为 WMI 数据的供应商后，WMI 内核模式组件就可以随时发送 WMI Irp。 WMI Irp 通常在用户模式数据使用者请求 WMI 数据时发送。

所有驱动程序都必须设置调度表入口点， [*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程才能处理 WMI 请求。

如果驱动程序通过调用[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)注册为 wmi 数据提供程序，则必须使用[处理 wmi 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)中所述的一种方法来处理 wmi irp。

未注册为 WMI 数据提供程序的驱动程序必须将所有 WMI 请求转发到下一个较低的驱动程序。

本部分介绍以下系统定义的 WMI 次要函数代码：

[**IRP\_MN\_更改\_单一\_实例**](irp-mn-change-single-instance.md)

[**IRP\_MN\_更改\_单一\_项**](irp-mn-change-single-item.md)

[**IRP\_MN\_禁用\_集合**](irp-mn-disable-collection.md)

[**IRP\_MN\_禁用\_事件**](irp-mn-disable-events.md)

[**IRP\_MN\_启用\_收集**](irp-mn-enable-collection.md)

[**IRP\_MN\_启用\_事件**](irp-mn-enable-events.md)

[**IRP\_MN\_EXECUTE\_方法**](irp-mn-execute-method.md)

[**IRP\_MN\_查询\_所有\_数据**](irp-mn-query-all-data.md)

[**IRP\_MN\_QUERY\_单一\_实例**](irp-mn-query-single-instance.md)

[**IRP\_MN\_REGINFO**](irp-mn-reginfo.md)

[**IRP\_MN\_REGINFO\_EX**](irp-mn-reginfo-ex.md)

如果驱动程序收到一个 IRP，其中包含任何其他 IRP 次要函数代码，则应将 IRP 转发到下一个较低版本的驱动程序。

 

 




