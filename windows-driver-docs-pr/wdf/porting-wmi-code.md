---
title: 移植 WMI
description: 移植 WMI
ms.assetid: 10843A15-3F6F-4DB5-A43B-4D9964DD3312
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94dce4edc0e10a58e701060d0ed5f721c7d86d26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842247"
---
# <a name="porting-wmi"></a>移植 WMI


\[仅适用于 KMDF\]

[**IRP\_MJ\_SYSTEM\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)请求表示对 WMI 数据的请求。 WDM 驱动程序通过实现[*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)函数并注册为 WMI 数据提供程序来处理此类请求。 不响应此类请求的 WDM 驱动程序实现一个*DispatchSystemControl*例程，只需将 irp 向下传递到下一个较低的驱动程序。

对于 KMDF 驱动程序，该框架为[**IRP\_MJ\_SYSTEM\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)提供默认处理。 不提供 WMI 数据的驱动程序不需要包括任何与 WMI 相关的代码。 相反，该框架会代表驱动程序将请求传递到下一个较低的驱动程序。

有关实现的详细信息，请参阅[在 KMDF 驱动程序中支持 WMI](supporting-wmi-in-kmdf-drivers.md)。

 

 





