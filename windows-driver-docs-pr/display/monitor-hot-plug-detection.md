---
title: 监视器热插拔检测
description: 监视器热插拔检测
ms.assetid: 170d2d5d-fd46-431d-9672-61fa048f7dd2
keywords:
- 视频存在 WDK 显示的网络，热插拔检测
- VidPN WDK 显示热插拔检测
- 视频输出连接器 WDK 视频存在网络
- HPD 感知 WDK 视频存在网络
- 热插拔检测 WDK 视频存在网络
- 拔出的检测 WDK 视频存在网络
- WDK 视频存在网络连接的监视器
- 未连接监视器 WDK 视频存在网络
- 未连接的监视器 WDK 视频存在网络
- 便携式计算机的视频输出 WDK 视频存在网络
- 移动计算机的视频输出 WDK 视频存在网络
- 监视器热插入检测 WDK 视频存在网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67fa574b01164ef151feb6823eb66068f1749eb0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323709"
---
# <a name="monitor-hot-plug-detection"></a>监视器热插拔检测


显示适配器上的视频输出被视为显示适配器的子设备。 监视器或其他外部显示器设备连接到的输出不被视为子设备。 在初始化，显示微型端口驱动程序期间[ **DxgkDdiQueryChildRelations** ](https://msdn.microsoft.com/library/windows/hardware/ff559750)函数指定每个子设备类型和 HPD 感知值。 类型为之一[ **DXGK\_子\_设备\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff561008)枚举器：

-   **TypeVideoOutput**

-   **TypeOther**

HPD 感知值是之一[ **DXGK\_子\_设备\_HPD\_感知**](https://msdn.microsoft.com/library/windows/hardware/ff561006)枚举器：

-   **HpdAwarenessAlwaysConnected**

-   **HpdAwarenessInterruptible**

-   **HpdAwarenessPolled**

具有一种类型的子设备**TypeVideoOutput**以外的其他任何 HPD 感知值**HpdAwarenessAlwaysConnected**称为*视频输出连接器*。

如果显示微型端口驱动程序无法确定监视器是否已连接到的视频输出，该驱动程序应 HPD 感知值设置为模拟的行为的不间断的设备， **HpdAwarenessInterruptible**。 如果显示微型端口驱动程序需要以指示不间断的监视器，应连接到的视频输出，例如当用户输入的键盘快捷方式，以切换到电视视图，该驱动程序应调用[ **DxgkCbIndicateChildStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff559522)起作用*ChildStatus*。**热插拔**。**连接**设置为**TRUE**。

在某些时候，操作系统请求显示微型端口驱动程序报告的具有的 HPD 感知值的所有视频输出连接器状态**HpdAwarenessPolled**。 没有任何固定的轮询时间间隔;相反，在没有更新可用的显示设备和模式的列表的特定需要时才发出请求。 例如，便携式计算机是在停靠时，操作系统需要知道监视器是否已连接到扩展坞上的视频输出。 通过调用显示微型端口驱动程序的操作系统发出的请求[ **DxgkDdiQueryChildStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff559754)函数为每个 HPD 感知值的子设备**HpdAwarenessPolled**。

具有的 HPD 感知值的视频输出连接器**HpdAwarenessInterruptible**，显示微型端口驱动程序负责每当热插入外部显示器设备通知操作系统或拔出。 显示微型端口驱动程序的中断处理代码调用显示端口驱动程序[ **DxgkCbIndicateChildStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff559522)函数的外部显示设备已连接到的报表或断开连接特定的视频输出。 当停靠便携式计算机，显示微型端口驱动程序[ *DxgkDdiNotifyAcpiEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff559695)函数必须调用**DxgkCbIndicateChildStatus**为在每个视频输出HPD 感知值扩展坞**HpdAwarenessInterruptible**。

如果使用 HPD 感知值的连接器**HpdAwarenessPolled**变得不可用 （即，遮住了） 停靠便携式计算机是，显示微型端口驱动程序*DxgkDdiNotifyAcpiEvent*函数必须调用**DxgkCbIndicateChildStatus**报告连接器已断开连接。

与便携式计算机上集成的显示面板相关联的视频输出是一个异常的情形。 操作系统需要知道便携式计算机盖是否打开或关闭，这样的想法*连接*用于表示打开和的理念*未连接*用于表示已关闭。 带有集成在便携式计算机上显示相关联的视频输出具有 HPD 感知值**HpdAwarenessInterruptible**。 但是，这并不意味着打开或关闭合上盖子时，会显示适配器产生中断。 相反，ACPI BIOS 会打开或关闭合上盖子时产生中断。 中断对显示微型端口驱动程序的调用中的结果[ *DxgkDdiNotifyAcpiEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff559695)函数，它调用**DxgkCbIndicateChildStatus**来报告状态（打开或关闭） 的合上盖子。 显示微型端口驱动程序通过设置报告的状态的合上盖子**HotPlug.Connected**的成员[ **DXGK\_子\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff561010)结构 **，则返回 TRUE** （打开） 或**FALSE** （关闭） 并传递 DXGK\_子\_状态结构**DxgkCbIndicateChildStatus**.

以下列表介绍监视器连接到一个 HD15 连接器，假定连接器具有一个 HPD 意识的值时遵循的步骤**HpdAwarenessPolled**。

1.  监视器连接到显示适配器上的 HD15 连接器。 显示适配器不会检测这为热即插即用事件。

2.  在未来某个时间，在用户模式应用程序请求的显示设备的列表。

3.  为 HPD 感知值的显示适配器上每个视频输出连接器**HpdAwarenessPolled**，VidPN 管理器会调用显示微型端口驱动程序[ **DxgkDdiQueryChildStatus**](https://msdn.microsoft.com/library/windows/hardware/ff559754)函数来确定是否已连接的外部显示设备。 当*DxgkDdiQueryChildStatus*称为 HD15 连接器，它报告外接显示器确实已连接。

以下列表介绍监视器连接到 DVI 连接器，则假定连接器具有一个 HPD 意识的值时遵循的步骤**HpdAwarenessInterruptible**。

1.  是液晶显示器连接到显示适配器上的 DVI 连接器。

2.  显示适配器检测到热即插即用事件，并生成中断。

3.  由显示微型端口驱动程序处理中断[ **DxgkDdiInterruptRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff559680)计划延迟的过程调用 (DPC) 的函数。 随后显示微型端口驱动程序的 DPC 回调函数进行调用。

4.  DPC 回调函数传递 DXGK\_子\_显示端口驱动程序的状态结构[ **DxgkCbIndicateChildStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff559522)函数以 DVI 状态报告连接器。 **ChildUid** DXGK 成员\_子\_状态结构标识 DVI 连接器，并且**HotPlug.Connected**成员 (设置为**TRUE**这种情况下) 指示外部显示器设备已连接。

假设 DVI 连接器支持硬件保护装置，具有三个分支：DVI、 HD15 和 S-视频。 在这种情况下，显示微型端口驱动程序将具有以前枚举三个与一个物理 DVI 连接器相关联的子设备：DVI 上 DVI、 HD15 上 DVI 和 S 视频上 DVI。 所有这些子设备具有的类型**TypeVideoOutput**且 HPD 感知值为**HpdAwarenessInterruptible**。 以下列表介绍监视器连接到硬件保护装置的 HD15 分支时遵循的步骤。

1.  显示适配器检测到热即插即用事件，并生成中断。

2.  由显示微型端口驱动程序处理中断[ **DxgkDdiInterruptRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff559680)计划延迟的过程调用 (DPC) 的函数。 随后显示微型端口驱动程序的 DPC 回调函数进行调用。

3.  DPC 回调函数将确定热即插即用事件的硬件保护装置 (HD15 上 DVI) HD15 分支上。

4.  DPC 回调函数传递 DXGK\_子\_状态结构[ **DxgkCbIndicateChildStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff559522)以在 DVI HD15 视频输出的状态报告。 **ChildUid** DXGK 成员\_子\_状态结构标识的视频输出，并且**HotPlug.Connected**成员 (设置为**TRUE**这种情况下) 指示外部显示器设备已连接。

以下列表介绍盖子便携式计算机上时遵循的步骤。

1.  合上盖子生成 ACPI 事件的便携式计算机上。 随后，在显示微型端口驱动程序[ *DxgkDdiNotifyAcpiEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff559695)调用函数。

2.  *DxgkDdiNotifyAcpiEvent*传递 DXGK\_子\_显示端口驱动程序的状态结构**DxgkCbIndicateChildStatus**函数来报告关联的子设备的状态与内置显示面板。 具体而言， *DxgkDdiNotifyAcpiEvent*设置**HotPlug.Connected** DXGK 成员\_子\_状态结构**FALSE**。

 

 





