---
title: 调用 WmiSystemControl 以处理 WMI IRP
description: 调用 WmiSystemControl 以处理 WMI IRP
ms.assetid: a2fa53e2-6468-4c3c-8b41-9a97305abc43
keywords:
- WMI WDK 内核请求
- 请求 WDK WMI
- Irp WDK WMI
- WmiSystemControl
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e02df29ea68f5f8ad56cbd0153185e10c252dd19
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338607"
---
# <a name="calling-wmisystemcontrol-to-handle-wmi-irps"></a>调用 WmiSystemControl 以处理 WMI IRP





WMI 库例程简化处理的 WMI 请求，因为驱动程序而不是处理每个此类请求，调用[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)。 在中**WmiSystemControl**调用时，驱动程序通过一个初始化[ **WMILIB\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff565813)到驱动程序的结构，其中包含入口点[WMI 库回调例程](https://msdn.microsoft.com/library/windows/hardware/ff566357)(*DpWmiXxx*例程) 以及有关驱动程序的数据块和事件块的信息。

由于 WMI 库提供传递动态实例名称或静态实例名称列表的机制，因此驱动程序可以使用 WMI 库来处理包含具有基于 PDO 或单个基名称字符串的静态实例名称的唯一数据块的请求。 有关静态和动态实例名称的详细信息，请参阅[定义 WMI 实例名](defining-wmi-instance-names.md)。 没有任何障碍的驱动程序由 WMI 库用于处理此类块的请求和处理请求，针对中的其他块，其[ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。 有关详细信息，请参阅[DispatchSystemControl 例程中处理 WMI Irp](processing-wmi-irps-in-a-dispatchsystemcontrol-routine.md)。

若要通过调用处理 WMI Irp **WmiSystemControl**，驱动程序必须实现某些所需*DpWmiXxx*回调例程，可能实现其他可选*DpWmiXxx*回调例程：

-   [*DpWmiQueryReginfo*](https://msdn.microsoft.com/library/windows/hardware/ff544097)—(Required) 提供有关数据和事件的信息会阻止正在注册驱动程序。 WMI 调用驾*DpWmiQueryReginfo*到进程例程[ **IRP\_MN\_REGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551731)或[ **IRP\_MN\_REGINFO\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff551734)请求。 有关详细信息，请参阅[使用 WMI 库对注册块](using-the-wmi-library-to-register-blocks.md)。

-   [*DpWmiQueryDataBlock*](https://msdn.microsoft.com/library/windows/hardware/ff544096)—(Required) 返回单一实例或数据块的所有实例。 WMI 调用驾*DpWmiQueryDataBlock*到进程例程[ **IRP\_MN\_查询\_单一\_实例**](https://msdn.microsoft.com/library/windows/hardware/ff551718)或[ **IRP\_MN\_查询\_所有\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff551650)请求。

-   [*DpWmiSetDataBlock*](https://msdn.microsoft.com/library/windows/hardware/ff544104)—(Optional) 更改的数据块的单个实例中的所有数据项。 WMI 调用驾*DpWmiSetDataBlock*到进程例程[ **IRP\_MN\_更改\_单一\_实例**](https://msdn.microsoft.com/library/windows/hardware/ff550831)请求。

-   [*DpWmiSetDataItem*](https://msdn.microsoft.com/library/windows/hardware/ff544108)—(Optional) 更改一个数据块的实例中的数据项。 WMI 调用的驱动程序*DpWmiSetDataItem*到进程例程[ **IRP\_MN\_更改\_单一\_项**](https://msdn.microsoft.com/library/windows/hardware/ff550836)请求。

-   [*DpWmiFunctionControl*](https://msdn.microsoft.com/library/windows/hardware/ff544094)—(Optional) 启用和禁用块注册为成本高昂，若要收集的事件通知和数据收集。 WMI 调用驾*DpWmiFunctionControl*到进程例程[ **IRP\_MN\_启用\_集合**](https://msdn.microsoft.com/library/windows/hardware/ff550857)， [**IRP\_MN\_禁用\_集合**](https://msdn.microsoft.com/library/windows/hardware/ff550848)， [ **IRP\_MN\_启用\_事件**](https://msdn.microsoft.com/library/windows/hardware/ff550859)，或[ **IRP\_MN\_禁用\_事件**](https://msdn.microsoft.com/library/windows/hardware/ff550851)请求。

-   [*DpWmiExecuteMethod*](https://msdn.microsoft.com/library/windows/hardware/ff544090)—(Optional) 执行与数据块关联的方法。 WMI 调用驾*DpWmiExecuteMethod*到进程例程[ **IRP\_MN\_EXECUTE\_方法**](https://msdn.microsoft.com/library/windows/hardware/ff550868)请求。

驱动程序的*DpWmiXxx*例程可以有选择的驱动程序编写器的任何名称。

然后再调用[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)，该驱动程序必须初始化[ **WMILIB\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff565813)条目的结构指向其*DpWmiXxx*例程和有关其数据块和事件块的信息。

当驱动程序收到的 WMI 请求：

1. 驱动程序调用**WmiSystemControl**用一个指针指向其初始化**WMILIB\_上下文**结构、 为其设备对象的指针和指向 IRP 的指针。

2. WMI 验证 IRP 参数和调用的驱动程序*DpWmiXxx*处理请求的例程。 如果该驱动程序中设置没有入口点及其**WMILIB\_上下文**可选*DpWmiXxx*例程，WMI 完成 IRP 用默认值和状态。

3. 在其*DpWmiXxx*例程，该驱动程序处理请求并将任何输出写入到调用方提供缓冲区。 例如，驱动程序的[ *DpWmiQueryDataBlock* ](https://msdn.microsoft.com/library/windows/hardware/ff544096)例程将指定的块的请求的实例写入到缓冲区。

4. 在所有*DpWmiXxx*之外例程[ *DpWmiQueryReginfo*](https://msdn.microsoft.com/library/windows/hardware/ff544097)，驱动程序调用[ **WmiCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff565798)以完成请求，则返回状态\_推迟完成时，与任何 IRP 的待决。

5. WMI 执行任何必要的后续处理时，包中相应的任何输出**WNODE\_* XXX*** 结构，并将输出和状态传递给数据使用者。

 

 




