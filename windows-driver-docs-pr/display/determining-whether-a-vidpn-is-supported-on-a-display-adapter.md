---
title: 确定显示适配器上的 VidPN 支持
description: 本主题介绍了显示微型端口驱动程序如何确定显示适配器是否支持特定视频网络（VidPN）。
ms.assetid: ebf001fb-e445-4534-8e89-60e1b06b2d6e
keywords:
- 视频显示网络 WDK 显示，确定是否受支持
- VidPN WDK 显示，确定是否支持
- 功能 VidPN WDK 显示
- 确定支持 VidPN 的 WDK 显示
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: d35fdb8cd02c485131a69f5e18d173fdc66156ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839750"
---
# <a name="determining-vidpn-support-on-a-display-adapter"></a>确定显示适配器上的 VidPN 支持


本主题介绍了显示微型端口驱动程序如何确定显示适配器是否支持特定视频网络（VidPN）。 阅读本资料前，应熟悉以下主题中的资料：

-   [视频显示网络简介](introduction-to-video-present-networks.md)

-   [VidPN 对象和接口](vidpn-objects-and-interfaces.md)

当 VidPN 满足以下条件时，它将*起作用*：

-   它有至少一个路径的拓扑。 （路径是源和目标之间的关联。）

-   拓扑中的每个源和目标都具有固定模式。

如果满足以下条件之一，则*在显示适配器上支持*VidPN：

-   它可以正常工作，并且可以在显示适配器上实现。 也就是说，可以将显示适配器上的视频输出编解码器配置为支持由 VidPN 指定的拓扑和固定模式。

-   它具有至少具有一个路径的拓扑，可以扩展到可在显示适配器上实现的功能 VidPN。 也就是说，无需更改已固定的任何模式，就可以固定所有视频现有源和尚未固定模式的目标的模式。 此外，还可以在显示适配器上实现生成的功能 VidPN。

-   它的拓扑为空。 其思路是，在显示适配器上始终支持不显示任何内容。

确定 vidpn 是否受支持的一部分是确定 VidPN 的拓扑是否有效。 换句话说，视频显示源能否连接到拓扑指定的视频显示目标？ 请注意，该拓扑中的所有视频目标都不需要连接的监视器。 拓扑可以是有效的，即使没有连接的监视器，也可以支持 VidPN。

VidPN 管理器会随时调用[**DxgkDdiIsSupportedVidPn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_issupportedvidpn)来询问显示适配器上是否支持特定 VidPN 的显示微型端口驱动程序。 传递给**DxgkDdiIsSupportedVidPn**的参数之一是被称为所需 VidPN 的 vidpn 对象的句柄。 **DxgkDdiIsSupportedVidPn**必须检查所需 vidpn 的拓扑，并且必须记下所需 vidpn 中的哪些视频现有源和目标已固定模式。 然后，它必须返回一个布尔值，该值指示是否支持所需的 VidPN （根据本主题前面给出的定义）。 有关检查 VidPN 的拓扑、源模式集和目标模式集的信息，请参阅[Vidpn 对象和接口](vidpn-objects-and-interfaces.md)。

 

 





