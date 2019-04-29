---
title: 视频呈现网络的术语
description: 视频呈现网络的术语
ms.assetid: a7a02522-de13-419f-8dc5-065943fd4645
keywords:
- 视频存在网络 WDK 显示中，术语
- VidPN WDK 显示中术语
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17d12c40803419d2f0e39ac3706bb35ecdac9dcf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365091"
---
# <a name="video-present-network-terminology"></a>视频呈现网络的术语


VidPN manager 使用视频存在网络 (VidPN) 的概念来管理组的显示设备连接到显示适配器。 有关详细信息，请参阅[简介视频存在网络](introduction-to-video-present-networks.md)。

以下列表提供了用于描述 VidPNs，显示适配器和设备建立连接以显示适配器的主要术语的定义。

<span id="display_adapter_s_presentational_subsystem"></span><span id="DISPLAY_ADAPTER_S_PRESENTATIONAL_SUBSYSTEM"></span>**显示适配器的是用于演示子系统**  
负责扫描的所有硬件都呈现来自视频内存并将其提供视频输出上的内容。

<span id="video_present_network"></span><span id="VIDEO_PRESENT_NETWORK"></span>**视频存在网络**  
显示适配器上的视频存在源与在适配器上的视频存在目标，并指定如何配置这些源和目标模型。 它是显示适配器是用于演示子系统的抽象。 VidPN 由以下内容组成：

<span id="video_present_sources"></span><span id="VIDEO_PRESENT_SOURCES"></span>**视频显示源**  
独立的视图 （即主图面上链） 可以同时显示显示适配器。

<span id="video_present_targets"></span><span id="VIDEO_PRESENT_TARGETS"></span>**视频显示目标**  
独立物理视频输出，显示适配器可以在其中每个呈现视图。

<span id="topology"></span><span id="TOPOLOGY"></span>**topology**  
一系列*视频存在路径*，其中每个视频的存在路径是视频显示源和视频的显示目标之间的关联。 视频显示路径指定一个特定的源连接到特定目标。 该路径还指定应用于已呈现内容的内容转换。 源连接到目标意味着显示适配器与源的主要的图面 （链） 中扫描，并将编码为视频信号格式为目标的扫描生成的内容应用 （例如，/亮度对比度提高内容转换闪烁筛选器，颜色转换） 过程中。

<span id="source_mode_sets"></span><span id="SOURCE_MODE_SETS"></span>**源模式设置**  
VidPN 中的每个视频存在源是与源模式集，这是主图面 VidPN 拓扑中的源支持的格式 （源模式） 的列表相关联。

<span id="target_mode_sets"></span><span id="TARGET_MODE_SETS"></span>**目标模式集**  
VidPN 中的每个视频显示目标是与目标模式集，这是在 VidPN 拓扑中的目标受支持的视频信号格式 （目标模式） 的列表相关联。

<span id="monitor_source_mode_sets"></span><span id="MONITOR_SOURCE_MODE_SETS"></span>**监视源模式设置**  
在连接到监视器 （或其他外部显示设备） VidPN 中的每个目标是与监视器源模式集，这是在已连接监视器上受支持的视频信号格式的列表相关联。

<span id="active_VidPN"></span><span id="active_vidpn"></span><span id="ACTIVE_VIDPN"></span>**active VidPN**  
当前设置将显示在适配器 VidPN。

<span id="pinned_mode"></span><span id="PINNED_MODE"></span>**固定的模式**  
一种模式指定为特定的视频显示源或目标所需模式。 固定 （目标） 的源的模式不一定是当前正在使用的是源 （目标）; 的模式而是在给定 VidPN 该源 （目标） 所需的模式 (可能是要用作下一步 active VidPN)。 固定的模式必须保持在整个 VidPN 上施加的其他约束设置其模式下可用。 也就是说，除非仍在修改后的 VidPN 支持所有的固定模式授权 VidPN 未更改。

<span id="functional_VidPN"></span><span id="functional_vidpn"></span><span id="FUNCTIONAL_VIDPN"></span>**功能 VidPN**  
VidPN 满足所有以下条件：

-   它必须包含至少一个视频存在路径的拓扑。

-   拓扑中的每个视频显示源都有固定的模式。

-   拓扑中的每个视频显示目标具有固定的模式。

<span id="modality"></span><span id="MODALITY"></span>**modality**  
VidPN 拓扑中，对于所有源和目标集模式下的集合。

<span id="cofunctional_mode_set"></span><span id="COFUNCTIONAL_MODE_SET"></span>**同时正常工作模式设置**  
这组可用于特定的源或目标，给定的约束 （例如，拓扑，其他源和目标上固定模式） 的模式的 VidPN。

<span id="cofunctional_VidPN_modality"></span><span id="cofunctional_vidpn_modality"></span><span id="COFUNCTIONAL_VIDPN_MODALITY"></span>**同时正常工作 VidPN 模态**  
VidPN 拓扑中，对于所有源和目标集同时正常工作模式的集合。

<span id="child_device_of_the_display_adapter"></span><span id="CHILD_DEVICE_OF_THE_DISPLAY_ADAPTER"></span>**显示适配器的子设备**  
一种设备上显示微型端口驱动程序枚举作为子级的显示适配器。 显示适配器的所有子设备都是板载设备;监视器和其他连接到设备的显示适配器不会考虑子设备。

<span id="external_device"></span><span id="EXTERNAL_DEVICE"></span>**外部设备**  
连接到子设备显示适配器的设备。 外部设备不会显示适配器的子设备。

<span id="video_output_device"></span><span id="VIDEO_OUTPUT_DEVICE"></span>**视频输出设备**  
提供到外部或内置的显示设备的视频输出信号的显示适配器子设备。

<span id="video_output_codec"></span><span id="VIDEO_OUTPUT_CODEC"></span>**输出视频编解码器**  
从主图面中的视频内存读取，并将该表面的视频信号表示形式放置在一个或多个显示适配器的视频输出的显示适配器上硬件编码器/解码器。

 
<span id="off_screen_memory"></span><span id="OFF_SCREEN_MEMORY"></span>**屏幕外内存**  
其内容不会出现在视频显示器的视频内存。 屏幕外内存可用于双缓冲，在其中需要大量图形操作的复杂的图形映像可以完全呈现显示前一种技术。 显示每个图像后，可以在相同的方式，提供一种有效的方法来实现动画中构造另一个映像。





