---
title: 监视器热插拔检测
description: 监视器热插拔检测
ms.assetid: 170d2d5d-fd46-431d-9672-61fa048f7dd2
keywords:
- 视频显示网络 WDK 显示，热插拔检测
- VidPN WDK 显示，热插拔检测
- 视频输出连接器 WDK 视频呈现网络
- HPD 感知 WDK 视频呈现网络
- 热插拔检测 WDK 视频呈现网络
- 未拔掉检测 WDK 视频显示网络
- 连接监视器 WDK 视频呈现网络
- 未连接监视 WDK 视频显示网络
- 未连接监视 WDK 视频呈现网络
- 便携计算机视频输出 WDK 视频显示网络
- 移动计算机视频输出 WDK 视频呈现网络
- 监视热插拔检测 WDK 视频呈现网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3b3826b62ac5efb80c7ca9d12dbb10adc8f2781
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066026"
---
# <a name="monitor-hot-plug-detection"></a>监视器热插拔检测

此页上的信息适用于使用 WDDM 版本2.2 之前的版本实现的图形驱动程序。

显示适配器上的视频输出被视为显示适配器的子设备。 连接到输出的监视器或其他外部显示设备不被视为子设备。 在初始化期间，显示微型端口驱动程序的 [**DxgkDdiQueryChildRelations**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_relations) 函数为每个子设备指定一个类型和一个 HPD 感知值。 该类型是 [**DXGK \_ 子 \_ 设备 \_ 类型**](/windows-hardware/drivers/ddi/dispmprt/ne-dispmprt-_dxgk_child_device_type) 枚举器之一：

-   **TypeVideoOutput**

-   **TypeOther**

HPD 感知值为 [**DXGK \_ 子 \_ 设备 \_ HPD \_ 感知**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgk_child_device_hpd_awareness) 枚举器之一：

-   **HpdAwarenessAlwaysConnected**

-   **HpdAwarenessInterruptible**

-   **HpdAwarenessPolled**

类型为 **TypeVideoOutput** 的子设备和除 **HpdAwarenessAlwaysConnected** 以外的任何 HPD 感知值称为 *视频输出连接器*。

如果显示微型端口驱动程序无法确定监视器是否连接到视频输出，驱动程序应模拟可中断设备的行为，并将 HPD 知晓值设置为 **HpdAwarenessInterruptible**。 如果显示微型端口驱动程序需要指示可中断的监视器应连接到视频输出，例如当用户输入键盘快捷方式切换到电视视图时，驱动程序应使用*ChildStatus*调用[**DxgkCbIndicateChildStatus**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_indicate_child_status)函数。**热插拔**。**已连接**设置为**TRUE**。

在某些情况下，操作系统会请求显示微型端口驱动程序报告 HPD 知晓值为 **HpdAwarenessPolled**的所有视频输出连接器的状态。 没有常规轮询间隔;相反，当有特定需要更新可用显示设备和模式的列表时，将发出请求。 例如，当插接便携式计算机时，操作系统需要知道监视器是否连接到扩展坞的视频输出。 操作系统通过为 HPD 感知值为**HpdAwarenessPolled**的每个子设备调用显示微型端口驱动程序的[**DxgkDdiQueryChildStatus**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_status)函数来发出请求。

对于 "HPD 感知" 值为 " **HpdAwarenessInterruptible**" 的视频输出连接器，显示微型端口驱动程序负责在热插拔或拔出外部显示设备时，通知操作系统。 显示微型端口驱动程序的中断处理代码将调用显示端口驱动程序的 [**DxgkCbIndicateChildStatus**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_indicate_child_status) 函数，以报告外部显示设备已连接到或已与特定视频输出断开连接。 当插接便携式计算机时，显示微型端口驱动程序的[*DxgkDdiNotifyAcpiEvent*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)函数必须为插接工作站上具有 HPD 感知值**HpdAwarenessInterruptible**的每个视频输出调用**DxgkCbIndicateChildStatus** 。

如果 "HPD 感知" 值为 " **HpdAwarenessPolled** " 的连接器变为不可用 (即，在插接便携式计算机时涵盖) ，则显示微型端口驱动程序的 *DxgkDdiNotifyAcpiEvent* 函数必须调用 **DxgkCbIndicateChildStatus** 以报告连接器已断开连接。

与便携式计算机上的集成显示面板相关联的视频输出是一个不寻常的情况。 操作系统需要知道便携式计算机的盖子是处于打开还是关闭状态，因此，" *连接* " 的思路用于表示开放，" *未连接* " 的思路用于表示闭合。 与便携计算机上的集成显示器关联的视频输出的 HPD 感知值为 **HpdAwarenessInterruptible**。 但这并不意味着显示适配器在盖子处于打开或关闭状态时生成中断。 相反，在打开或关闭盖子时，ACPI BIOS 会生成一个中断。 此中断会导致调用显示微型端口驱动程序的 [*DxgkDdiNotifyAcpiEvent*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event) 函数，该函数将调用 **DxgkCbIndicateChildStatus** 来报告盖子 (打开或关闭) 的状态。 显示微型端口驱动程序通过将[**DXGK \_ 子 \_ 状态**](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_child_status)结构的**热连接**成员设置为**TRUE**来报告盖子的状态， (打开) 或**FALSE** (关闭) 并将 DXGK \_ 子 \_ 状态结构传递到**DxgkCbIndicateChildStatus**。

下面的列表介绍了在监视器连接到 HD15 连接器时遵循的步骤，假设连接器的 HPD 感知值为 **HpdAwarenessPolled**。

1.  监视器连接到显示适配器上的 HD15 连接器。 显示适配器不会将此作为热插拔事件进行检测。

2.  在将来的某个时间，用户模式应用程序会请求显示设备的列表。

3.  对于显示适配器上 HPD 感知值为 **HpdAwarenessPolled**的每个视频输出连接器，VidPN 管理器会调用显示微型端口驱动程序的 [**DxgkDdiQueryChildStatus**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_status) 函数来确定外部显示设备是否已连接。 为 HD15 连接器调用 *DxgkDdiQueryChildStatus* 时，它会报告外部监视器确实已连接。

以下列表描述了在监视器连接到 DVI 连接器时遵循的步骤，假设连接器的 HPD 感知值为 **HpdAwarenessInterruptible**。

1.  平面面板连接到显示适配器上的 DVI 连接器。

2.  显示适配器检测热插拔事件，并生成中断。

3.  中断由显示微型端口驱动程序的 [**DxgkDdiInterruptRoutine**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine) 函数进行处理，该函数计划 (DPC) 的延迟过程调用。 随后，将调用显示微型端口驱动程序的 DPC 回调函数。

4.  DPC 回调函数 \_ \_ 向显示端口驱动程序的 [**DXGKCBINDICATECHILDSTATUS**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_indicate_child_status) 函数传递 DXGK 子状态结构，以报告 DVI 连接器的状态。 DXGK **ChildUid** \_ 子状态结构的 CHILDUID 成员 \_ 标识 DVI 连接器，而**热连接**的成员 (设置为**TRUE** ，在这种情况下) 指示外部显示设备已连接。

假设某个 DVI 连接器支持具有三个分支的转换器： DVI、HD15 和 S-视频。 在这种情况下，显示微型端口驱动程序之前已枚举了三个与一个物理 DVI 连接器关联的子设备： dvi、HD15、dvi-i 和 S-video。 其中每个子设备的类型为 **TypeVideoOutput** ，HPD 感知值为 **HpdAwarenessInterruptible**。 以下列表描述了将监视器连接到转换器的 HD15 分支时遵循的步骤。

1.  显示适配器检测热插拔事件，并生成中断。

2.  中断由显示微型端口驱动程序的 [**DxgkDdiInterruptRoutine**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine) 函数进行处理，该函数计划 (DPC) 的延迟过程调用。 随后，将调用显示微型端口驱动程序的 DPC 回调函数。

3.  DPC 回调函数确定热插拔事件位于 (HD15-DVI) 的转换器的 HD15 分支上。

4.  DPC 回调函数将 DXGK \_ 子 \_ 状态结构传递到 [**DxgkCbIndicateChildStatus**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_indicate_child_status) ，以报告 HD15-DVI 视频输出的状态。 DXGK **ChildUid** \_ 子状态结构的 ChildUid 成员 \_ 标识视频输出，在这种情况下，"**热连接**" 成员 (设置为**TRUE**) 指示外部显示设备已连接。

以下列表描述了在便携式计算机上关闭盖子时遵循的步骤。

1.  在便携式计算机上关闭盖子，这会生成 ACPI 事件。 随后，将调用显示微型端口驱动程序的 [*DxgkDdiNotifyAcpiEvent*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event) 函数。

2.  *DxgkDdiNotifyAcpiEvent* 将 DXGK \_ 子 \_ 状态结构传递到显示端口驱动程序的 **DxgkCbIndicateChildStatus** 函数，以报告与内置显示面板关联的子设备的状态。 具体而言， *DxgkDdiNotifyAcpiEvent* 将 DXGK 子状态结构的 **已连接的已连接** 成员设置 \_ \_ 为 **FALSE**。

 

