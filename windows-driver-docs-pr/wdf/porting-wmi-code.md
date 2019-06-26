---
title: 移植 WMI
description: 移植 WMI
ms.assetid: 10843A15-3F6F-4DB5-A43B-4D9964DD3312
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77fab706be9335b7bbbe811e40dba799934ec99a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379643"
---
# <a name="porting-wmi"></a>移植 WMI


\[仅适用于 KMDF\]

[ **IRP\_MJ\_系统\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)请求表示对 WMI 数据的请求。 WDM 驱动程序通过实现来处理此类请求[ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)函数，并注册为 WMI 数据提供程序。 不应对此类请求的 WDM 驱动程序实现*DispatchSystemControl*只是将传递到下一个较低的驱动程序 Irp 的例程。

用于 KMDF 驱动程序，该框架提供默认处理[ **IRP\_MJ\_系统\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)。 不提供 WMI 数据的驱动程序不需要包括任何 WMI 相关的代码。 相反，框架将请求传递到下一个较低的驱动程序代表该驱动程序。

有关实现的详细信息，请参阅[KMDF 驱动程序中支持 WMI](supporting-wmi-in-kmdf-drivers.md)。

 

 





