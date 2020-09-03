---
title: 移植 WMI
description: 移植 WMI
ms.assetid: 10843A15-3F6F-4DB5-A43B-4D9964DD3312
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04153eeadd054bb4bba424bb065da3b491ad50f5
ms.sourcegitcommit: 057b72e8a44ba8f4282e072edc7be0b7e9341d2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89412486"
---
# <a name="porting-wmi"></a>移植 WMI


\[仅适用于 KMDF\]

[**IRP \_ MJ \_ 系统 \_ 控制**](../kernel/irp-mj-system-control.md)请求表示对 WMI 数据的请求。 WDM 驱动程序通过实现 [*DispatchSystemControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 函数并注册为 WMI 数据提供程序来处理此类请求。 不响应此类请求的 WDM 驱动程序实现一个 *DispatchSystemControl* 例程，只需将 irp 向下传递到下一个较低的驱动程序。

对于 KMDF 驱动程序，该框架为 [**IRP \_ MJ \_ 系统 \_ 控件**](../kernel/irp-mj-system-control.md)提供默认处理。 不提供 WMI 数据的驱动程序不需要包括任何与 WMI 相关的代码。 相反，该框架会代表驱动程序将请求传递到下一个较低的驱动程序。

有关实现的详细信息，请参阅 [在 KMDF 驱动程序中支持 WMI](introduction-to-wmi-for-kmdf-drivers.md)。

 

