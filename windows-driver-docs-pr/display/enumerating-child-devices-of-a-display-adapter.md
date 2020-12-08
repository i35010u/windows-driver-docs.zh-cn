---
title: 枚举显示适配器的子设备
description: 枚举显示适配器的子设备
keywords:
- 视频显示网络 WDK 显示，显示适配器子设备
- VidPN WDK 显示，显示适配器子设备
- 子设备 WDK 视频呈现网络
- 显示适配器子设备 WDK 视频呈现网络
- 枚举子设备 WDK 视频呈现网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 464b12ef935b9fb124196cc61b7a51b82aff4b98
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832765"
---
# <a name="enumerating-child-devices-of-a-display-adapter"></a>枚举显示适配器的子设备


下面的一系列步骤说明了显示端口驱动程序、显示微型端口驱动程序和视频显示网络 (VidPN) manager 在初始化时协作，以枚举显示适配器的子设备。

1.  显示端口驱动程序调用显示微型端口驱动程序的 [**DxgkDdiStartDevice**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device) 函数。 *DxgkDdiStartDevice* 在 *NumberOfChildren* 参数中返回 (，)  (显示适配器的子) 子适配器的设备数。 *DxgkDdiStartDevice* 还会在 *NumberOfVideoPresentSources* 参数中返回 (，) 显示适配器所支持的视频显示源的第 N 个。 随后，这些视频源会由数字0，1，.。。N-1。

2.  显示端口驱动程序调用显示端口驱动程序的 [**DxgkDdiQueryChildRelations**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_relations) 函数，该函数枚举显示适配器的子设备。 *DxgkDdiQueryChildRelations* 填充 [**DXGK \_ 子 \_ 描述符**](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_child_descriptor) 结构的数组：每个子设备一个。 请注意，显示适配器的所有子设备都在板上：连接到显示适配器的监视器和其他外部设备不被视为子设备。 有关详细信息，请参阅 [显示适配器的子设备](child-devices-of-the-display-adapter.md)。 *DxgkDdiQueryChildRelations* 必须枚举潜在的子设备，以及在初始化时物理存在的子设备。 例如，如果将便携式计算机连接到扩展坞将导致新视频输出的外观，则 *DxgkDdiQueryChildRelations* 必须枚举该视频输出，而不考虑计算机在初始化时是否停靠。 此外，如果将连接器连接到视频输出连接器将允许多个监视器共享连接器，则 *DxgkDdiQueryChildRelations* 必须枚举每个转换器分支的子设备，而不考虑转换器是否在初始化时连接。

3.  对于每个子设备 (按步骤 1) 中所述进行枚举，此值为 **HpdAwarenessInterruptible** 或 **HpdAwarenessPolled**，显示端口驱动程序会调用显示微型端口驱动程序的 [**DxgkDdiQueryChildStatus**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_status) 函数来确定子设备是否有连接的外部设备。

4.  显示端口驱动程序为满足以下条件之一的每个子设备创建一个 PDO：
    -   子设备的 HPD 感知值为 **HpdAwarenessAlwaysConnected**。
    -   子设备的 HPD 感知值为 **HpdAwarenessPolled** 或 **HpdAwarenessInterruptible**，操作系统从上一个查询或通知子设备已连接到外部设备。

5.  显示端口驱动程序为每个满足以下条件之一的子设备调用显示微型端口驱动程序的 [**DxgkDdiQueryDeviceDescriptor**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_device_descriptor) 函数：

    -   已知子设备已连接外部设备。
    -   假定子设备已连接外部设备。
    -   子设备的类型为 **TypeOther**。

    如果连接的监视器 (或其他显示设备) 支持 EDID 描述符， *DxgkDdiQueryDeviceDescriptor* 将返回扩展的显示信息数据 (EDID) 块。

    注意：在初始化期间，显示端口驱动程序对每个监视器调用 *DxgkDdiQueryDeviceDescriptor* ，以获取监视器 EDID 的第一个128字节块。 这为显示端口驱动程序在初始化时所需的内容： PnP 硬件 ID、实例 ID、兼容 Id 和设备文本。 稍后，monitor 类函数驱动程序 ( # A0) 为每个监视器调用 *DxgkDdiQueryDeviceDescriptor* ，以获取第一个128字节的 edid 块和额外的128字节 edid 扩展块。 这意味着将调用显示微型端口驱动程序两次，以提供每个监视器 EDID 的第一个128字节块。

6.  VidPN 管理器会为显示适配器支持的所有视频源和视频提供目标获取标识符。 视频显示源由数字0，1，.。。N-1，其中 N 是显示微型端口驱动程序的 *DxgkDdiStartDevice* 函数返回的源的数目。 视频显示目标具有唯一的整数标识符，这些标识符之前是在 *DxgkDdiQueryChildRelations* 过程中由显示微型端口驱动程序创建的。 **TypeVideoOutput** 类型的每个子设备都与视频显示目标相关联，子设备的 DXGK 子描述符结构的 **ChildUid** 成员 \_ \_ 将用作视频显示目标的标识符。

7.  VidPN 管理器使用以下过程来生成初始 VidPN。
    -   如果在注册表中记录了最后一个已知良好的 VidPN，请将其用作初始 VidPN。

    -   否则，调用显示微型端口驱动程序的 [**DxgkDdiRecommendFunctionalVidPn**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn) 函数以获取初始 VidPN。

    -   如果 *DxgkDdiRecommendFunctionalVidPn* 未能返回可接受的功能 vidpn，请创建包含一个视频显示路径的简单 vidpn;这就是一个 (源，目标) 对。 调用显示微型端口驱动程序的 [**DxgkDdiIsSupportedVidPn**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_issupportedvidpn) 函数，验证建议的 VidPN 是否正常工作。 如果 *DxgkDdiIsSupportedVidPn* 报告建议的 vidpn 将不起作用，请继续尝试，直到找到合适的 vidpn。

    -   调用显示微型端口驱动程序的 [**DxgkDdiEnumVidPnCofuncModality**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality) 函数来确定适用于 VidPN 的源和目标模式。

 

