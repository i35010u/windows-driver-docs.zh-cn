---
title: 视频呈现网络的术语
description: 视频呈现网络的术语
ms.assetid: a7a02522-de13-419f-8dc5-065943fd4645
keywords:
- 视频显示网络 WDK 显示，术语
- VidPN WDK 显示，术语
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17d12c40803419d2f0e39ac3706bb35ecdac9dcf
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242892"
---
# <a name="video-present-network-terminology"></a>视频呈现网络的术语


VidPN 管理器使用视频呈现网络（VidPN）的概念来管理连接到显示适配器的显示设备集。 有关详细信息，请参阅[视频显示网络简介](introduction-to-video-present-networks.md)。

下面的列表提供了用于描述 VidPNs、显示适配器以及连接到显示适配器的设备的主要术语的定义。

<span id="display_adapter_s_presentational_subsystem"></span><span id="DISPLAY_ADAPTER_S_PRESENTATIONAL_SUBSYSTEM"></span>**显示适配器的 presentational 子系统**  
所有负责扫描视频内存中呈现的内容并将其显示在视频输出上的硬件。

<span id="video_present_network"></span><span id="VIDEO_PRESENT_NETWORK"></span>**视频呈现网络**  
一种将显示适配器上的视频显示源关联到适配器上的视频显示目标的模型，并指定如何配置这些源和目标。 它是显示适配器的 presentational 子系统的抽象。 VidPN 包含以下各项：

<span id="video_present_sources"></span><span id="VIDEO_PRESENT_SOURCES"></span>**视频显示源**  
显示适配器可并发显示的独立视图（即主表面链）。

<span id="video_present_targets"></span><span id="VIDEO_PRESENT_TARGETS"></span>**视频显示目标**  
独立物理视频输出，其中每个显示适配器都可以显示视图。

<span id="topology"></span><span id="TOPOLOGY"></span>**拓扑**  
*视频*显示路径的集合，其中每个视频显示路径是视频显示源与视频显示目标之间的关联。 视频显示路径指定特定源连接到特定目标。 该路径还指定了对所显示内容应用的内容转换。 将源连接到目标意味着显示适配器从源的主表面（链）进行扫描，并将扫描的内容编码为目标的视频信号格式，在过程中应用内容转换（例如，对比度/亮度提高、闪烁过滤器、颜色转换）。

<span id="source_mode_sets"></span><span id="SOURCE_MODE_SETS"></span>**源模式集**  
VidPN 中的每个视频显示源都与源模式集相关联，这是在 VidPN 拓扑中的源上支持的主表面格式（源模式）的列表。

<span id="target_mode_sets"></span><span id="TARGET_MODE_SETS"></span>**目标模式集**  
VidPN 中的每个视频显示目标都与目标模式集相关联，后者是在 VidPN 拓扑中的目标上支持的视频信号格式（目标模式）的列表。

<span id="monitor_source_mode_sets"></span><span id="MONITOR_SOURCE_MODE_SETS"></span>**监视源模式集**  
连接到监视器（或其他外部显示设备）的 VidPN 中的每个目标都与监视器源模式集相关联，该模式集是连接的监视器上支持的视频信号格式的列表。

<span id="active_VidPN"></span><span id="active_vidpn"></span><span id="ACTIVE_VIDPN"></span>**活动 VidPN**  
显示适配器上当前设置的 VidPN。

<span id="pinned_mode"></span><span id="PINNED_MODE"></span>**固定模式**  
指定为特定视频显示源或目标的所需模式的模式。 源（目标）上固定的模式不一定是源（目标）当前使用的模式;相反，它是给定 VidPN 中该源（目标）所需的模式（可能用作下一个活动 VidPN）。 固定模式必须在对 VidPN 施加的其他约束中的模式设置中保持可用。 也就是说，除非修改后的 VidPN 仍支持所有固定模式，否则不会对 VidPN 进行任何更改。

<span id="functional_VidPN"></span><span id="functional_vidpn"></span><span id="FUNCTIONAL_VIDPN"></span>**功能 VidPN**  
满足以下所有条件的 VidPN：

-   它有至少一个视频显示路径的拓扑。

-   拓扑中的每个视频显示源都具有固定模式。

-   拓扑中的每个视频显示目标都有固定模式。

<span id="modality"></span><span id="MODALITY"></span>**模态**  
VidPN 的拓扑中所有源和目标的模式集集。

<span id="cofunctional_mode_set"></span><span id="COFUNCTIONAL_MODE_SET"></span>**cofunctional 模式集**  
针对特定源或目标可用的一组模式，给定 VidPN 的约束（例如，拓扑、固定在其他源和目标上的模式）。

<span id="cofunctional_VidPN_modality"></span><span id="cofunctional_vidpn_modality"></span><span id="COFUNCTIONAL_VIDPN_MODALITY"></span>**cofunctional VidPN 模态**  
Cofunctional 模式的集合在 VidPN 的拓扑中为所有源和目标设置。

<span id="child_device_of_the_display_adapter"></span><span id="CHILD_DEVICE_OF_THE_DISPLAY_ADAPTER"></span>**显示适配器的子设备**  
显示适配器上显示的微型端口驱动程序将其枚举为子项的设备。 显示适配器的所有子设备都是板载设备;连接到显示适配器的监视器和其他设备不被视为子设备。

<span id="external_device"></span><span id="EXTERNAL_DEVICE"></span>**外部设备**  
连接到显示适配器的子设备的设备。 外部设备不被视为显示适配器的子设备。

<span id="video_output_device"></span><span id="VIDEO_OUTPUT_DEVICE"></span>**视频输出设备**  
显示适配器的子设备，它向外部或内置显示设备提供视频输出信号。

<span id="video_output_codec"></span><span id="VIDEO_OUTPUT_CODEC"></span>**视频输出编解码器**  
显示适配器上的硬件编码器/解码器，从视频内存的主表面进行读取，并在一个或多个显示适配器的视频输出上放置该表面的视频信号表示形式。

 
<span id="off_screen_memory"></span><span id="OFF_SCREEN_MEMORY"></span>**离屏内存**  
其内容未显示在视频显示器上的视频内存。 离屏内存可用于双缓冲，这种方法在显示时，需要大量图形操作的复杂图形图像可以完全呈现。 显示每个图像后，可以采用相同方式构造另一个图像，从而提供一种有效的方式来实现动画。





