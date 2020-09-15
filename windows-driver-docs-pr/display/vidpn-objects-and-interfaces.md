---
title: VidPN 对象和接口
description: VidPN 对象和接口
ms.assetid: 5dedac8c-9a99-4b3a-81be-39819135cd97
keywords:
- 视频显示网络 WDK 显示，对象
- VidPN WDK 显示，对象
- 对象 WDK 视频呈现网络
- 接口 WDK 视频呈现网络
- 视频显示网络 WDK 显示，接口
- VidPN WDK 显示，接口
- 子对象 WDK 视频呈现网络
ms.date: 10/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: b5abcec089cfc533be5b5456459613aff60c1317
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106520"
---
# <a name="vidpn-objects-and-interfaces"></a>VidPN 对象和接口


视频呈现网络 (VidPN) manager 使用 VidPN 对象维护有关视频现有源、视频显示目标和显示模式之间的关联的信息。 有关详细信息，请参阅 [视频显示网络简介](introduction-to-video-present-networks.md) 主题。

## <a name="vidpn-object"></a>VidPN 对象

VidPN 对象包含以下子对象。

-   拓扑

-   源模式集

-   目标模式集

-   监视源模式集

-   监视频率范围集

-   监视器描述符集

-   路径

-   Source

-   目标

-   源模式

-   目标模式

-   监视源模式

下图说明了 VidPN 对象及其子对象。

![阐释 vidpn 对象及其子对象的关系图](images/vidpnobject.png)

前面的关系图说明了特定的关联是一对一、一对多、多对一还是多对多的。 例如，关系图显示一个源可以属于多个路径，但一个目标只能属于一个路径。

关系图中的蓝色对象是通过句柄和接口访问的，而灰色对象则通过结构指针进行访问。 此上下文中的接口是包含函数指针的结构。 例如， [**DXGK \_ VIDPNTOPOLOGY \_ 接口**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface) 结构包含指向由 VidPN 管理器实现的函数 (的指针) 由显示微型端口驱动程序调用来检查和更改拓扑对象。 当显示微型端口驱动程序调用其中任何一个函数时，它必须提供拓扑对象的句柄。 下表列出了用于访问 VidPN 对象及其子对象的句柄、接口和指针数据类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">对象</th>
<th align="left">访问方法和数据类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Vidpn (VidPN 接口) </p></td>
<td align="left"><p>通过句柄和接口进行访问。</p>
<p>D3DKMDT_HVIDPN</p>
<p><a href="/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface" data-raw-source="[&lt;strong&gt;DXGK_VIDPN_INTERFACE&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface)"><strong>DXGK_VIDPN_INTERFACE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>VidPN 拓扑接口 (拓扑) </p></td>
<td align="left"><p>通过句柄和接口进行访问。</p>
<p>D3DKMDT_HVIDPNTOPOLOGY</p>
<p><a href="/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface" data-raw-source="[&lt;strong&gt;DXGK_VIDPNTOPOLOGY_INTERFACE&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface)"><strong>DXGK_VIDPNTOPOLOGY_INTERFACE</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>源模式设置 (VidPN 源模式集接口) </p></td>
<td align="left"><p>通过句柄和接口进行访问。</p>
<p>D3DKMDT_HVIDPNSOURCEMODESET</p>
<p><a href="/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpnsourcemodeset_interface" data-raw-source="[&lt;strong&gt;DXGK_VIDPNSOURCEMODESET_INTERFACE&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpnsourcemodeset_interface)"><strong>DXGK_VIDPNSOURCEMODESET_INTERFACE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>目标模式集 (VidPN 目标模式集接口) </p></td>
<td align="left"><p>通过句柄和接口进行访问。</p>
<p>D3DKMDT_HVIDPNTARGETMODESET</p>
<p><a href="/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntargetmodeset_interface" data-raw-source="[&lt;strong&gt;DXGK_VIDPNTARGETMODESET_INTERFACE&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntargetmodeset_interface)"><strong>DXGK_VIDPNTARGETMODESET_INTERFACE</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>监视源模式集</p></td>
<td align="left"><p>通过句柄和接口进行访问。</p>
<p>D3DKMDT_HMONITORSOURCEMODESET</p>
<p><a href="/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_monitorsourcemodeset_interface" data-raw-source="[&lt;strong&gt;DXGK_MONITORSOURCEMODESET_INTERFACE&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_monitorsourcemodeset_interface)"><strong>DXGK_MONITORSOURCEMODESET_INTERFACE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>路径</p></td>
<td align="left"><p>通过结构指针访问。</p>
<p><a href="/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path" data-raw-source="[&lt;strong&gt;D3DKMDT_VIDPN_PRESENT_PATH&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path)"><strong>D3DKMDT_VIDPN_PRESENT_PATH</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>源</p></td>
<td align="left"><p>通过结构指针访问。</p>
<p><a href="/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_present_source" data-raw-source="[&lt;strong&gt;D3DKMDT_VIDEO_PRESENT_SOURCE&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_present_source)"><strong>D3DKMDT_VIDEO_PRESENT_SOURCE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>目标</p></td>
<td align="left"><p>通过结构指针访问。</p>
<p><a href="/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_present_target" data-raw-source="[&lt;strong&gt;D3DKMDT_VIDEO_PRESENT_TARGET&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_present_target)"><strong>D3DKMDT_VIDEO_PRESENT_TARGET</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>源模式</p></td>
<td align="left"><p>通过结构指针访问。</p>
<p><a href="/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_source_mode" data-raw-source="[&lt;strong&gt;D3DKMDT_VIDPN_SOURCE_MODE&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_source_mode)"><strong>D3DKMDT_VIDPN_SOURCE_MODE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>目标模式</p></td>
<td align="left"><p>通过结构指针访问。</p>
<p><a href="/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_target_mode" data-raw-source="[&lt;strong&gt;D3DKMDT_VIDPN_TARGET_MODE&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_target_mode)"><strong>D3DKMDT_VIDPN_TARGET_MODE</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>监视源模式</p></td>
<td align="left"><p>通过结构指针访问。</p>
<p><a href="/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_monitor_source_mode" data-raw-source="[&lt;strong&gt;D3DKMDT_MONITOR_SOURCE_MODE&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_monitor_source_mode)"><strong>D3DKMDT_MONITOR_SOURCE_MODE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>监视频率范围集</p></td>
<td align="left"><p>通过结构指针访问。</p>
<p>[<strong>DXGK_MONITORFREQUENCYRANGESET_INTERFACE </strong>] (/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_monitorfrequencyrangeset_interface) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>监视器描述符集</p></td>
<td align="left"><p>通过结构指针访问。</p>
<p>[<strong>DXGK_MONITORDESCRIPTORSET_INTERFACE</strong>] (/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_monitordescriptorset_interface) </p></td>
</tr>
</tbody>
</table>

## <a name="vidpn-manager"></a>VidPN 管理器

VidPN 管理器是 DirectX 图形内核子系统的组件之一，会带有用于构建和维护 VidPNs 的显示微型端口驱动程序。 以下步骤介绍了显示微型端口驱动程序如何获取一个句柄和一个到 VidPN 对象的接口。

1.  在初始化期间，DirectX 图形内核子系统将调用显示微型端口驱动程序的 [*DxgkDdiStartDevice*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device) 函数。 该调用为显示微型端口驱动程序提供了 [**DXGKRNL \_ 接口**](/windows-hardware/drivers/ddi/index) 结构，其中包含了由 DirectX 图形内核子系统实现的函数的指针。 其中一项功能是 [*DxgkCbQueryVidPnInterface*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_queryvidpninterface)。

2.  在某些时候，VidPN 管理器需要显示微型端口驱动程序的帮助，因此它通过调用以下函数之一向显示微型端口驱动程序提供 VidPN 对象的句柄：
    -   [*DxgkDdiIsSupportedVidPn*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_issupportedvidpn)
    -   [*DxgkDdiRecommendFunctionalVidPn*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)
    -   [*DxgkDdiEnumVidPnCofuncModality*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)

3.  显示微型端口驱动程序将步骤2中获取的句柄传递给 [*DxgkCbQueryVidPnInterface*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_queryvidpninterface)，后者将返回指向 [**DXGK \_ VIDPN \_ 接口**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface) 结构的指针。

在显示微型端口驱动程序具有指向 VidPN 对象的句柄和接口后，它可以根据需要获取 (的句柄和接口) 到主子对象：拓扑、源模式集、目标模式集和监视源模式集。 例如，显示微型端口驱动程序可以 (VidPN 接口) 中的一个函数调用 [*pfnGetTopology*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_gettopology) ，以获取 vidpn 拓扑对象的句柄和指向 [**DXGK \_ VIDPNTOPOLOGY \_ 接口**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface) 结构的指针。

以下函数 (VidPN 接口) 提供对 VidPN 对象的主要子对象的句柄和接口。

-   [*pfnGetTopology*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_gettopology)
-   [*pfnAcquireSourceModeSet*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_acquiresourcemodeset)
-   [*pfnAcquireTargetModeSet*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_acquiretargetmodeset)

请注意，前面的列表中的两个函数具有释放 VidPN 子对象的对应函数。

-   [*pfnReleaseSourceModeSet*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_releasesourcemodeset)

-   [*pfnReleaseTargetModeSet*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_releasetargetmodeset)

显示微型端口驱动程序获取一个句柄和一个 VidPNs 主子对象的接口后，它可以调用接口函数以获取与子对象相关的对象的描述符。 例如，给定拓扑对象的句柄和接口，显示微型端口驱动程序可以执行以下步骤来获取拓扑中所有路径的描述符。

1.  [VidPN 拓扑接口](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface)

    调用 VidPN 拓扑接口的 [*pfnAcquireFirstPathInfo*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntopology_acquirefirstpathinfo) 函数，以获取一个指向 [**D3DKMDT \_ VidPN \_ 显示 \_ 路径**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path) 结构的指针，该结构描述拓扑中的第一个路径。

2.  [VidPN 拓扑接口](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface)

    重复调用 [*pfnAcquireNextPathInfo*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntopology_acquirenextpathinfo) 函数，以获取指向用于 \_ \_ \_ 描述拓扑中剩余路径的 D3DKMDT VIDPN 显示路径结构的指针。

同样，显示微型端口驱动程序可以通过调用以下任一模式集接口的 *pfnAcquireFirstModeInfo* 和 *pfnAcquireNextModeInfo* 函数，来获取模式集中的模式描述符。

-   [**DXGK \_ VIDPNSOURCEMODESET \_ 接口**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpnsourcemodeset_interface)

-   [**DXGK \_ VIDPNTARGETMODESET \_ 接口**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntargetmodeset_interface)

-   [**DXGK \_ MONITORSOURCEMODESET \_ 接口**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_monitorsourcemodeset_interface)

请注意， [**DXGK \_ VIDPNSOURCEMODESET \_ 接口**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpnsourcemodeset_interface) 接口没有用于从源模式集中删除模式的函数。 当显示微型端口驱动程序需要更新源模式集时，它不会通过添加和删除模式改变现有模式集。 相反，它会创建新的模式集来替换旧模式集。 必须更新模式集的函数的一个示例是显示微型端口驱动程序的 [*DxgkDdiEnumVidPnCofuncModality*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality) 函数。 更新源模式集所涉及的步骤如下所示：

1.  调用[**DXGK \_ VIDPNSOURCEMODESET \_ 接口**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpnsourcemodeset_interface)接口的[*pfnCreateNewModeInfo*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_createnewmodeinfo) ，以获取指向由 vidpn 管理器) 分配 (的[**D3DKMDT \_ VIDPN \_ 源 \_ 模式**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_source_mode)结构的指针。

    重复调用 [*pfnAddMode*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_addmode) ，将模式添加到源模式集。

2.  调用[**DXGK \_ VIDPN \_ 接口**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface)的[*pfnAssignSourceModeSet*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_assignsourcemodeset)函数，以将新模式集分配给特定视频现有源。 新源模式集会替换当前分配给该源的源模式集。

更新目标模式集类似于更新源模式集。 [**DXGK \_ VIDPNTARGETMODESET \_ 接口**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntargetmodeset_interface)接口具有以下功能：

-   [VidPN 目标模式集接口](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_target_mode)

    用于创建新的目标模式集的 [*pfnCreateNewModeInfo*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntargetmodeset_createnewmodeinfo) 函数，以及用于将模式添加到该集的 [*pfnAddMode*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntargetmodeset_addmode) 函数。

没有用于获取属于特定路径的源和目标的函数 (集) 。 显示微型端口驱动程序可以通过检查代表路径的[**D3DKMDT \_ VIDPN \_ 显示 \_ 路径**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path)结构的**VidPnSourceId**和**VidPnTargetId**成员来确定哪些源和目标属于特定路径。

## <a name="see-also"></a>另请参阅

[确定显示适配器是否支持 VidPN](determining-whether-a-vidpn-is-supported-on-a-display-adapter.md)

[枚举协同工作的 VidPN 源和目标模式](enumerating-cofunctional-vidpn-source-and-target-modes.md)

[视频呈现网络的术语](video-present-network-terminology.md)

[获取其他监视目标模式](obtaining-additional-monitor-target-modes.md)