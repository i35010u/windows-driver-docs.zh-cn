---
title: 确定显示适配器上的 VidPN 支持
description: 本主题介绍如何显示微型端口驱动程序确定显示适配器是否支持特定的视频存在网络 (VidPN)。
ms.assetid: ebf001fb-e445-4534-8e89-60e1b06b2d6e
keywords:
- 视频存在网络 WDK 显示，请确定是否支持
- VidPN WDK 显示，确定是否支持
- 功能 VidPN WDK 显示
- 确定 VidPN 支持 WDK 显示
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: f132b5c7d3db0264e77ce5d615aef2dd2eff927f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384882"
---
# <a name="determining-vidpn-support-on-a-display-adapter"></a>确定显示适配器上的 VidPN 支持


本主题介绍如何显示微型端口驱动程序确定显示适配器是否支持特定的视频存在网络 (VidPN)。 在阅读此材料之前, 应该熟悉以下主题中的材料：

-   [简介视频存在网络](introduction-to-video-present-networks.md)

-   [VidPN 对象和接口](vidpn-objects-and-interfaces.md)

是 VidPN*功能*如果它满足以下条件：

-   它必须包含至少一个路径的拓扑。 （路径为源和目标之间的关联。）

-   每个源和目标在拓扑中的有固定的模式。

是 VidPN*上显示适配器支持*如果以下条件之一为 true:

-   其可以正常工作，并在上的显示适配器实现。 即，显示适配器上的视频输出编解码器可以配置为支持的拓扑，VidPN 由指定的固定的模式。

-   它已包含至少一个路径的拓扑，它可以扩展到可以显示适配器实现的功能 VidPN。 也就是说，很有可能，而无需更改已固定，任何模式为所有视频显示源和尚不具有固定的模式的目标上的 pin 模式。 此外，它就可能显示适配器上实现生成功能 VidPN。

-   它具有空的拓扑。 其思路是，显示任何内容均始终支持显示适配器上。

在确定是否支持 VidPN 确定 VidPN 的拓扑是否有效。 换而言之，可以存在的视频源连接到指定拓扑的视频存在目标？ 请注意，它不要求在拓扑中的所有视频显示目标已连接监视器。 拓扑可以是有效的并且可以支持 VidPN，即使没有连接的监视器。

有时，VidPN 管理器调用[ **DxgkDdiIsSupportedVidPn** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_issupportedvidpn)询问是否显示适配器上支持某些 VidPN 显示微型端口驱动程序。 一个参数传递给**DxgkDdiIsSupportedVidPn**是名为所需的 VidPN VidPN 对象的句柄。 **DxgkDdiIsSupportedVidPn**必须检查所需 VidPN 拓扑和必须记下这些视频显示源和目标中所需 VidPN 已经具有固定模式。 然后，它必须返回一个布尔值，该值指示是否将所需的 VidPN 支持 （根据本主题中前面提供的定义）。 有关检查拓扑、 源模式集和目标的 VidPN 模式集的信息，请参阅[VidPN 对象和接口](vidpn-objects-and-interfaces.md)。

 

 





