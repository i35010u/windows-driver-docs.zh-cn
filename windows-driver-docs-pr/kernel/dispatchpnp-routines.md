---
title: DispatchPnP 例程
description: DispatchPnP 例程
ms.assetid: 909d99ac-5bd3-4b12-bfb4-79713cf2a156
keywords:
- 调度例程 WDK 内核，DispatchPnP 例程
- DispatchPnP 例程
- 即插即用的调度例程 WDK 内核
- Irp WDK 内核，插调度例程
- 插调度例程 WDK 内核
- IRP_MJ_PNP I/O 函数代码
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c1b30ac3ae9f9ae697c6c61fd7fecb9ab2f5f45
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566783"
---
# <a name="dispatchpnp-routines"></a>DispatchPnP 例程





驱动程序的[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程支持[插](implementing-plug-and-play.md)通过处理 Irp 为[ **IRP\_MJ\_PNP** ](https://msdn.microsoft.com/library/windows/hardware/ff550772) I/O 函数代码。 与相关联**IRP\_MJ\_PNP**函数代码是几个小的 I/O 函数代码 (请参阅[即插即用和播放次要 Irp](https://msdn.microsoft.com/library/windows/hardware/ff558807))，某些必须处理的所有驱动程序和一些这可以根据需要处理。 PnP 管理器使用这些次要函数代码直接驱动程序来启动、 停止和删除的设备和查询有关他们的设备的驱动程序。

设备的所有驱动程序必须有机会处理 PnP Irp 对于设备，除了在少数情况下允许函数或筛选器驱动程序失败 IRP 的位置。

每个驱动程序*DispatchPnP*例程必须遵循下列规则：

-   函数或筛选器驱动程序必须通过向设备堆栈中下一步的驱动程序 PnP Irp，除非该函数或筛选器驱动程序处理 IRP，并在遇到失败 （由于没有足够的资源，例如）。

    设备的所有驱动程序必须有机会处理 PnP Irp 的设备，除非的驱动因素之一时遇到错误。 PnP 管理器将 Irp 发送到设备堆栈中的顶部驱动程序。 函数和筛选器驱动程序传递到下一步的驱动程序，IRP，父总线驱动程序完成 IRP。 请参阅[向下设备堆栈传递 PnP Irp](passing-pnp-irps-down-the-device-stack.md)有关详细信息。

    驱动程序可能会失败 IRP，如果它尝试处理 IRP，并且在遇到错误 （如资源不足）。 如果驱动程序接收 IRP，它无法处理代码，该驱动程序必须无法 IRP。 应用程序必须通过此类 IRP 到下一步的驱动程序而无需修改 IRP 的状态。

-   驱动程序必须处理某些 PnP Irp，可能会根据需要处理其他人。

    每个即插即用驱动程序需要处理某些 Irp，如[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738)，并可以根据需要处理其他人。 请参阅[即插即用和播放次要 Irp](https://msdn.microsoft.com/library/windows/hardware/ff558807)有关哪些 Irp 的必需和可选的每一类驱动程序 （函数驱动程序、 筛选器驱动程序和总线驱动程序）。

    驱动程序可以故障所需的 PnP IRP，相应的错误状态，但驱动程序不能返回状态\_不\_支持此类 IRP。

-   如果驱动程序已成功处理 PnP IRP，驱动程序将 IRP 状态设置为成功。 它不依赖于另一个驱动程序堆栈设置的状态中。

    驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功通知即插即用经理驱动程序已成功处理 IRP。 对于某些 Irp，非总线驱动程序可能能够依赖于其父总线驱动程序将状态设置为成功。 但是，这是一种有风险的做法。 以保持一致性和可靠性，驱动程序必须设置 IRP 状态为成功它已成功处理每个 PnP IRP。

-   如果驱动程序失败 IRP，驱动程序完成 IRP 具有错误状态，并不会传递到下一步的驱动程序 IRP。

    无法像 IRP [ **IRP\_MN\_查询\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551725)，驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_未成功。 其他错误的其他 Irp 的状态值包括状态\_不足\_资源和状态\_无效\_设备\_状态。

    驱动程序未设置状态\_不\_它们处理 Irp 的支持。 这是由即插即用管理器设置的初始状态。 如果 IRP 完成，此状态，则表示堆栈中的没有驱动程序处理 IRP;所有驱动程序只被传递给下一步的驱动程序的 IRP。

-   驱动程序必须在处理其 （在向设备堆栈下的 IRP 的方法） 的调度例程中 PnP IRP [ **IoCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程 （上 IRP 的方式重新启动设备堆栈)，或同时指定参考中IRP 的页。

    一些 PnP Irp，如[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738)，按设备堆栈顶部的驱动程序，然后按每个下一步低驱动程序必须首先处理。 其他人，例如[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)，必须首先处理由父总线驱动程序。 还有一些业务负责人，如[ **IRP\_MN\_查询\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff551664)，可以重新启动设备堆栈下的方法和方法处理。 请参阅[即插即用和播放次要 Irp](https://msdn.microsoft.com/library/windows/hardware/ff558807)将应用于每个 PnP IRP 的规则。 请参阅[推迟 PnP IRP 处理直到较低的驱动程序完成](postponing-pnp-irp-processing-until-lower-drivers-finish.md)处理父总线驱动程序必须首先处理的 PnP Irp 的相关信息。

-   驱动程序必须将信息添加到 IRP 的向下设备堆栈上 IRP 和修改或删除备份的 IRP 的方式的信息。

    PnP IRP 查询响应中返回的信息，驱动程序必须遵循此约定，可以使有序地按设备的分层驱动程序传递的信息。

-   除了明确的说明文档，其中一个驱动程序必须不依赖于 PnP Irp 正在按任何特定顺序发送。

-   当驱动程序发送 PnP IRP 时，它必须将 IRP 发送到设备堆栈中的顶部驱动程序。

    大多数 PnP Irp 发送的即插即用管理器中，但一些可以由驱动程序 (例如， [ **IRP\_MN\_查询\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff551687))。 驱动程序必须将 PnP IRP 发送到设备堆栈顶部的驱动程序。 调用[ **IoGetAttachedDeviceReference** ](https://msdn.microsoft.com/library/windows/hardware/ff549145)指针设备对象为获取该驱动程序在设备堆栈的顶部。

应测试与已检验版本操作系统的驱动程序。 系统已检验的版本验证驱动程序是否遵循众多上面列出的即插即用规则。

 

 




