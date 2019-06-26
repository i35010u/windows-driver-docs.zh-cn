---
title: WMI 次要 IRP
description: WMI 次要 IRP
ms.date: 08/12/2017
ms.assetid: 5788294f-2145-4381-9b06-3b138b2d26df
ms.localizationpriority: medium
ms.openlocfilehash: d48d8b56fb1bd07a33eadb22b3847c7a9ff51936
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353788"
---
# <a name="wmi-minor-irps"></a>WMI 次要 IRP





本部分介绍[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi) Irp 的 WDM 的 WMI 扩展的一部分。 所有 WMI Irp 使用的主要代码[ **IRP\_MJ\_系统\_控制**](irp-mj-system-control.md)和细微的代码，指示特定的 WMI 请求。 WMI 内核模式组件可以发送 WMI Irp 任何驱动程序的成功注册后作为供应商的 WMI 数据的时间。 通常 WMI Irp 获取发送时的用户模式数据使用者已请求 WMI 数据。

所有驱动程序必须设置的调度表入口点[ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程来处理 WMI 请求。

如果驱动程序将注册为 WMI 数据提供程序通过调用[ **IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)，则它必须处理使用一种技术中所述的 WMI Irp[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests).

不将注册为 WMI 数据提供程序的驱动程序必须转发到下一步低驱动程序的所有 WMI 请求。

本部分介绍以下系统定义 WMI 次要函数代码：

[**IRP\_MN\_更改\_单个\_实例**](irp-mn-change-single-instance.md)

[**IRP\_MN\_更改\_单个\_项**](irp-mn-change-single-item.md)

[**IRP\_MN\_禁用\_集合**](irp-mn-disable-collection.md)

[**IRP\_MN\_DISABLE\_EVENTS**](irp-mn-disable-events.md)

[**IRP\_MN\_ENABLE\_COLLECTION**](irp-mn-enable-collection.md)

[**IRP\_MN\_ENABLE\_EVENTS**](irp-mn-enable-events.md)

[**IRP\_MN\_EXECUTE\_METHOD**](irp-mn-execute-method.md)

[**IRP\_MN\_查询\_所有\_数据**](irp-mn-query-all-data.md)

[**IRP\_MN\_查询\_单个\_实例**](irp-mn-query-single-instance.md)

[**IRP\_MN\_REGINFO**](irp-mn-reginfo.md)

[**IRP\_MN\_REGINFO\_EX**](irp-mn-reginfo-ex.md)

如果该驱动程序接收 IRP 包含任何其他 IRP 次要函数代码，它应转发到下一步低驱动程序 IRP。

 

 




