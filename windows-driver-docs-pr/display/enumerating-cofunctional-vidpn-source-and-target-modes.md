---
title: 枚举协同工作的 VidPN 源和目标模式
description: 枚举协同工作的 VidPN 源和目标模式
ms.assetid: f1aa6277-7af6-4ba0-8ff1-d562f7029540
keywords:
- 视频显示网络 WDK 显示，枚举目标和源模式
- VidPN WDK 显示，枚举目标和源模式
- 约束 VidPN WDK
- 枚举目标和源模式 WDK 视频呈现网络
- 源模式 WDK 视频呈现网络
- 目标模式 WDK 视频呈现网络
- 固定缩放转换 WDK 视频呈现网络
- 固定旋转转换 WDK 视频呈现网络
- 多级多级显示的音频视频网络
- 模式设置 WDK 视频呈现网络
- 检查约束 VidPN WDK
- 缩放支持标志 WDK 视频呈现网络
- 旋转支持标志 WDK 视频呈现网络
- 枚举透视 WDK 视频呈现网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9439dfaa1b0a5d32c60be6d55dcbef801ec613ff
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065866"
---
# <a name="enumerating-cofunctional-vidpn-source-and-target-modes"></a>枚举协同工作的 VidPN 源和目标模式


本主题介绍视频显示网络 (VidPN) manager 和显示器微型端口驱动程序如何协作，以枚举视频显示源和目标上可用的模式。 阅读本资料前，应熟悉以下主题中的资料：

-   [视频呈现网络简介](introduction-to-video-present-networks.md)

-   [VidPN 对象和接口](vidpn-objects-and-interfaces.md)

VidPN 管理器随时会要求显示的微型端口驱动程序枚举显示适配器的视频显示源和目标上可用的模式。 通常，请求采用以下模式：

1.  VidPN 管理器创建或获取一个 VidPN，其中包含固定在其所有源和目标上的模式。

2.  VidPN 管理器调用 [**DxgkDdiIsSupportedVidPn**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_issupportedvidpn) 来确定是否可以扩展 vidpn，以形成在显示适配器上支持的功能 vidpn。 也就是说，它会询问是否可以在剩余的源和目标上固定模式，而无需更改现有固定模式。

3.  VidPN 管理器调用 [**DxgkDdiEnumVidPnCofuncModality**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality) 来获取在尚未固定模式的源和目标上可用的模式。

传递给 *DxgkDdiEnumVidPnCofuncModality* 的参数之一是名为 "约束 vidpn" 的 VidPN 对象的句柄。

*DxgkDdiEnumVidPnCofuncModality* 必须执行以下操作：

-   检查约束 VidPN。

-   对于没有固定模式的每个源和目标，请调整模式集，使其成为与约束 cofunctional 的最大可能模式集。

-   对于没有固定缩放转换的每个路径，请调整缩放支持标志，使其与约束 cofunctional。

-   对于没有固定旋转转换的每个路径，请调整旋转支持标志，使其与约束 cofunctional。

-   对于具有固定模式的每个源，会报告可用于该源的多级多级方法。

以下各段介绍了如何执行上一个项目符号列表中的每个任务。

### <a name="span-idinspecting_the_constraining_vidpnspanspan-idinspecting_the_constraining_vidpnspaninspecting-the-constraining-vidpn"></a><span id="inspecting_the_constraining_vidpn"></span><span id="INSPECTING_THE_CONSTRAINING_VIDPN"></span>检查约束 VidPN

约束 VidPN 的以下属性是必须由 *DxgkDdiEnumVidPnCofuncModality*使用的约束。

-   拓扑 (源和目标之间的关联集) 

-   固定模式

-   每个路径的缩放、支持、旋转和旋转支持

-   每个路径的目标颜色基数

-   目标颜色系数每个路径的动态范围

-   每个路径 (图形或视频) 的内容类型

-   每个路径的伽玛斜坡

若要从约束 VidPN 中提取约束，请执行以下步骤：

-   首先调用 [**pfnGetTopology**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_gettopology) 函数，以获取一个指向 [vidpn 拓扑接口](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface) 的指针，该接口表示约束 VidPN 的拓扑。

-   调用 [**pfnAcquireFirstPathInfo**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntopology_acquirefirstpathinfo) 和 [**pfnAcquireNextPathInfo**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntopology_acquirenextpathinfo) 函数以获取有关约束 VidPN 的拓扑中的每个路径的信息。 有关特定路径 (源 ID、目标 ID、缩放转换、旋转转换、目标颜色基础等等 ) ）的信息包含在 [**D3DKMDT \_ VIDPN \_ 显示 \_ 路径**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path) 结构中。

-   对于每个路径，将路径的源 ID 传递到 [**pfnAcquireSourceModeSet**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_acquiresourcemodeset) 函数，以获取路径的源。

-   调用 [**pfnAcquirePinnedModeInfo**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_acquirepinnedmodeinfo) 函数以确定在源的模式集中固定任何)  (模式。 如果源的模式集具有固定模式，则可能无需检查集中的其余模式。 如果该模式集没有固定模式，请通过调用 [**pfnAcquireFirstModeInfo**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_acquirefirstmodeinfo) 和 [**pfnAcquireNextModeInfo**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_acquirenextmodeinfo)检查该集中的其余模式。

    使用类似的过程来检查目标模式集并确定哪些目标模式集具有固定模式。

### <a name="span-idadjusting_mode_setsspanspan-idadjusting_mode_setsspanadjusting-mode-sets"></a><span id="adjusting_mode_sets"></span><span id="ADJUSTING_MODE_SETS"></span>调整模式集

当检查与约束 VidPN 的拓扑中的源和目标相关联的模式集时，请记下哪些模式集具有固定模式。 如果某个模式集没有固定模式，则确定是否需要调整它。 如果模式集包含与约束不 cofunctional 的模式，或者它缺少与约束 cofunctional 的可用模式，则必须对其进行调整。

对于已连接监视器的视频显示目标，还必须考虑监视器支持的模式集。 即使显示适配器上的视频显示目标支持特定模式 (给定的约束) ，如果连接的监视器也支持模式，则只应在目标的模式集内列出此模式。 若要确定连接的监视器支持的模式，请执行以下步骤：

-   [DXGK \_ 监视器接口](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_monitor_interface)

    调用 [**pfnAcquireMonitorSourceModeSet**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_acquiremonitorsourcemodeset)。 如果模式集无需调整，则可以将其保留原样。 如果需要调整模式集，则必须创建新的模式集，并将现有模式集替换为新模式集。

-   [DXGK_VIDPN_INTERFACE](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface)

    若要创建和填充新源模式集，请调用 [**pfnCreateNewSourceModeSet**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_createnewsourcemodeset)。

-   [_DXGK_VIDPNSOURCEMODESET_INTERFACE](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpnsourcemodeset_interface)

    然后调用 [**pfnCreateNewModeInfo**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_createnewmodeinfo) 和 [**pfnAddMode**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_addmode)。

-   [DXGK_VIDPN_INTERFACE](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface)

    最后调用 [**pfnAssignSourceModeSet**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_assignsourcemodeset) ，将现有的源模式集替换为新的。

### <a name="adjusting-scaling-support-flags"></a>调整缩放支持标志

对于约束 VidPN 的拓扑中的每个路径，确定路径是否具有固定的缩放变换。 若要进行确定，请检查 *vpnPath*。**ContentTransformation**，其中 *vpnPath* 是表示路径的 [**D3DKMDT \_ VIDPN \_ 显示 \_ 路径**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path) 结构。 如果为 *vpnPath*。**ContentTransformation** 设置为 **D3DKMDT \_ VPPS \_ IDENTITY**、 **D3DKMDT \_ VPPS \_ 居中**或 **D3DKMDT \_ VPPS \_ 伸展**，然后固定路径的缩放变换。 否则，不会固定缩放变换。

如果路径没有固定缩放转换，则确定是否需要调整路径的缩放支持标志。 如果支持标志显示对不 cofunctional 约束的缩放类型的支持，或者无法显示与约束 cofunctional 的缩放类型支持，则必须对其进行调整。 若要更改缩放支持标志，请设置包含标志的 [**D3DKMDT \_ VIDPN \_ 显示 \_ 路径 \_ 缩放 \_ 支持**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling_support) 结构的成员。

### <a name="adjusting-rotation-support-flags"></a>调整旋转支持标志

调整路径的旋转支持标志类似于调整路径的缩放支持标志。 假设 *vpnPath* 是 D3DKMDT \_ VIDPN \_ 显示 \_ 路径结构。 如果为 *vpnPath*。**ContentTransformation** 设置为 **D3DKMDT \_ VPPR \_ IDENTITY**、 **D3DKMDT \_ VPPR \_ ROTATE90**、 **D3DKMDT \_ VPPR \_ ROTATE180**或 **D3DKMDT \_ VPPR \_ ROTATE270**，然后固定路径的旋转转换。 否则，不会固定旋转转换。 旋转支持标志在 *vpnPath*中。**ContentTransformation. RotationSupport**。

### <a name="span-idreporting_multisampling_methodsspanspan-idreporting_multisampling_methodsspanreporting-multisampling-methods"></a><span id="reporting_multisampling_methods"></span><span id="REPORTING_MULTISAMPLING_METHODS"></span>报表多级方法

如果显示适配器有一个或多个视频输出编解码器，这些编解码器能够通过多级的消除锯齿功能，则必须为具有固定模式的每个源报告 (给定约束) 的多级取样方法。 若要报告可用的多级取样方法，请执行以下步骤：

-   创建 [D3DDDI \_ MULTISAMPLINGMETHOD](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_multisamplingmethod) 结构的数组
-   将数组传递给[VidPN 接口](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface)的[**pfnAssignMultisamplingMethodSet**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_assignmultisamplingmethodset)函数。

[D3DDDI \_ MULTISAMPLINGMETHOD](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_multisamplingmethod)结构有两个成员，您必须对其进行设置，这将对多级采样方法进行特征化。 **采样数**成员指示取样的 subpixels 数。 **NumQualityLevels**成员指示该方法可以操作的质量级别数。 可以指定任意数量的质量级别，只要 noticably 级别的每个增加都会提高所提供图像的质量。

### <a name="span-idenumeration_pivotsspanspan-idenumeration_pivotsspanenumeration-pivots"></a><span id="enumeration_pivots"></span><span id="ENUMERATION_PIVOTS"></span>枚举透视

如前文所述， *DxgkDdiEnumVidPnCofuncModality* 必须创建与在其 *hConstrainingVidPn* 参数中传递的 VidPN cofunctional 的模式集。 在某些情况下， *DxgkDdiEnumVidPnCofuncModality* 必须根据附加信息 (*EnumPivotType* 和 *EnumPivot* 参数中传递的枚举透视) 增加其行为。

枚举 pivot 可以是以下项之一：

-   特定视频显示源的模式集

-   特定视频显示目标的模式集

-   特定 VidPN 显示路径的缩放转换

-   特定 VidPN 显示路径的旋转转换

如果枚举透视为模式集，则 *DxgkDdkEnumVidPnCofuncModality* 必须使该模式设置保持不变。 如果枚举透视是 (旋转) 转换路径时的缩放，则 *DxgkDdiEnumVidPnCofuncModality* 不得更改该路径) 支持标志 (旋转。

 

