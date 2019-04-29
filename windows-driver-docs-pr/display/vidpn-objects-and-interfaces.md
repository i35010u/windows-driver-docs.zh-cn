---
title: VidPN 对象和接口
description: VidPN 对象和接口
ms.assetid: 5dedac8c-9a99-4b3a-81be-39819135cd97
keywords:
- 视频存在网络 WDK 显示中，对象
- VidPN WDK 显示中对象
- 对象 WDK 视频存在网络
- 接口 WDK 视频存在网络
- 视频存在网络 WDK 显示，接口
- VidPN WDK 显示接口
- 子对象 WDK 视频存在网络
ms.date: 10/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 83a153440ba05804fcbf0ebc159e083183b93aab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391219"
---
# <a name="vidpn-objects-and-interfaces"></a>VidPN 对象和接口


视频存在网络 (VidPN) 管理器使用 VidPN 对象来维护有关视频显示源、 视频显示目标和显示模式之间的关联的信息。 有关详细信息，请参阅[简介视频存在网络](introduction-to-video-present-networks.md)主题。

## <a name="vidpn-object"></a>VidPN 对象

VidPN 对象包含以下子对象。

-   拓扑

-   源模式设置

-   目标模式设置

-   监视源模式设置

-   监视频率范围组

-   监视器描述符集

-   路径

-   Source

-   目标

-   源模式

-   目标模式

-   监视器源模式

下图说明了 VidPN 对象和及其子对象。

![说明 vidpn 对象和及其子对象的关系图](images/vidpnobject.png)

上图显示在特定的关联是一对一、 多对多对一或多对多。 例如，图显示了一个源可以属于多个路径，但目标只能属于只有一条路径。

在关系图中的蓝色对象访问通过句柄和接口，并通过结构指针访问灰色对象。 在此上下文中的接口是包含函数指针的结构。 例如， [ **DXGK\_VIDPNTOPOLOGY\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff562091)结构包含指向函数 （由 VidPN manager 实现） 的指针的显示微型端口驱动程序调用以检查并更改拓扑对象。 当显示微型端口驱动程序调用这些函数之一时，它必须提供拓扑对象的句柄。 下表列出了用于访问 VidPN 对象和及其子对象的句柄、 接口和指针数据类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Object</th>
<th align="left">访问方法和数据类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>VidPN （VidPN 接口）</p></td>
<td align="left"><p>访问通过句柄和接口。</p>
<p>D3DKMDT_HVIDPN</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562108" data-raw-source="[&lt;strong&gt;DXGK_VIDPN_INTERFACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562108)"><strong>DXGK_VIDPN_INTERFACE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>拓扑 （VidPN 拓扑接口）</p></td>
<td align="left"><p>访问通过句柄和接口。</p>
<p>D3DKMDT_HVIDPNTOPOLOGY</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562091" data-raw-source="[&lt;strong&gt;DXGK_VIDPNTOPOLOGY_INTERFACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562091)"><strong>DXGK_VIDPNTOPOLOGY_INTERFACE</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>源模式设置 （VidPN 源模式设置接口）</p></td>
<td align="left"><p>访问通过句柄和接口。</p>
<p>D3DKMDT_HVIDPNSOURCEMODESET</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562073" data-raw-source="[&lt;strong&gt;DXGK_VIDPNSOURCEMODESET_INTERFACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562073)"><strong>DXGK_VIDPNSOURCEMODESET_INTERFACE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>设置目标模式 （VidPN 目标模式设置接口）</p></td>
<td align="left"><p>访问通过句柄和接口。</p>
<p>D3DKMDT_HVIDPNTARGETMODESET</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562082" data-raw-source="[&lt;strong&gt;DXGK_VIDPNTARGETMODESET_INTERFACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562082)"><strong>DXGK_VIDPNTARGETMODESET_INTERFACE</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>监视源模式设置</p></td>
<td align="left"><p>访问通过句柄和接口。</p>
<p>D3DKMDT_HMONITORSOURCEMODESET</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561921" data-raw-source="[&lt;strong&gt;DXGK_MONITORSOURCEMODESET_INTERFACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561921)"><strong>DXGK_MONITORSOURCEMODESET_INTERFACE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>路径</p></td>
<td align="left"><p>访问通过结构的指针。</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546647" data-raw-source="[&lt;strong&gt;D3DKMDT_VIDPN_PRESENT_PATH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546647)"><strong>D3DKMDT_VIDPN_PRESENT_PATH</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Source</p></td>
<td align="left"><p>访问通过结构的指针。</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546614" data-raw-source="[&lt;strong&gt;D3DKMDT_VIDEO_PRESENT_SOURCE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546614)"><strong>D3DKMDT_VIDEO_PRESENT_SOURCE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>目标</p></td>
<td align="left"><p>访问通过结构的指针。</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546617" data-raw-source="[&lt;strong&gt;D3DKMDT_VIDEO_PRESENT_TARGET&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546617)"><strong>D3DKMDT_VIDEO_PRESENT_TARGET</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>源模式</p></td>
<td align="left"><p>访问通过结构的指针。</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546724" data-raw-source="[&lt;strong&gt;D3DKMDT_VIDPN_SOURCE_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546724)"><strong>D3DKMDT_VIDPN_SOURCE_MODE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>目标模式</p></td>
<td align="left"><p>访问通过结构的指针。</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546729" data-raw-source="[&lt;strong&gt;D3DKMDT_VIDPN_TARGET_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546729)"><strong>D3DKMDT_VIDPN_TARGET_MODE</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>监视器源模式</p></td>
<td align="left"><p>访问通过结构的指针。</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546133" data-raw-source="[&lt;strong&gt;D3DKMDT_MONITOR_SOURCE_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546133)"><strong>D3DKMDT_MONITOR_SOURCE_MODE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>监视频率范围组</p></td>
<td align="left"><p>访问通过结构的指针。</p>
<p>[<strong>DXGK_MONITORFREQUENCYRANGESET_INTERFACE</strong> ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_monitorfrequencyrangeset_interface)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>监视器描述符集</p></td>
<td align="left"><p>访问通过结构的指针。</p>
<p>[<strong>DXGK_MONITORDESCRIPTORSET_INTERFACE</strong>](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_monitordescriptorset_interface)</p></td>
</tr>
</tbody>
</table>

## <a name="vidpn-manager"></a>VidPN Manager

所以，就会显示微型端口驱动程序来构建和维护 VidPNs 与协作 VidPN 管理器，它是 DirectX 图形内核子系统的组件之一。 以下步骤介绍如何显示微型端口驱动程序获取句柄和 VidPN 对象的接口。

1.  在初始化期间，DirectX 图形内核子系统调用显示微型端口驱动程序[ *DxgkDdiStartDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff560775)函数。 调用提供了显示微型端口驱动程序与[ **DXGKRNL\_界面**](https://msdn.microsoft.com/library/windows/hardware/ff560940)结构，其中包含指向由 DirectX 图形内核子系统实现的函数的指针。 这些功能之一是[ *DxgkCbQueryVidPnInterface*](https://msdn.microsoft.com/library/windows/hardware/ff559553)。

2.  在某些时候，VidPN manager 需要显示微型端口驱动程序的帮助，因此它提供了显示微型端口驱动程序的句柄 VidPN 对象通过调用下列函数之一：
    -   [*DxgkDdiIsSupportedVidPn*](https://msdn.microsoft.com/library/windows/hardware/ff559684)
    -   [*DxgkDdiRecommendFunctionalVidPn*](https://msdn.microsoft.com/library/windows/hardware/ff559775)
    -   [*DxgkDdiEnumVidPnCofuncModality*](https://msdn.microsoft.com/library/windows/hardware/ff559649)

3.  显示微型端口驱动程序将传递到步骤 2 中获取的句柄[ *DxgkCbQueryVidPnInterface*](https://msdn.microsoft.com/library/windows/hardware/ff559553)，这会返回一个指向[ **DXGK\_VIDPN\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff562108)结构。

显示微型端口驱动程序具有一个句柄和 VidPN 对象的接口后，它可以对主要的子对象获取句柄和接口 （如需要）： 拓扑、 源模式集、 目标模式设置和监视源模式设置。 例如，显示微型端口驱动程序可以调用[ *pfnGetTopology* ](https://msdn.microsoft.com/library/windows/hardware/ff562854) （VidPN 接口中的函数之一） 以获取 VidPN 拓扑对象的句柄和指向的[ **DXGK\_VIDPNTOPOLOGY\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff562091)结构。

（中的 VidPN 接口） 的以下函数提供句柄和 VidPN 对象的主要子对象的接口。

-   [*pfnGetTopology*](https://msdn.microsoft.com/library/windows/hardware/ff562854)
-   [*pfnAcquireSourceModeSet*](https://msdn.microsoft.com/library/windows/hardware/ff562110)
-   [*pfnAcquireTargetModeSet*](https://msdn.microsoft.com/library/windows/hardware/ff562113)

请注意，上面的列表中的函数的两个具有相应的函数 VidPN 子对象的该版本。

-   [*pfnReleaseSourceModeSet*](https://msdn.microsoft.com/library/windows/hardware/ff562855)

-   [*pfnReleaseTargetModeSet*](https://msdn.microsoft.com/library/windows/hardware/ff562858)

显示微型端口驱动程序将获取一个句柄并对某一 VidPNs 主子对象的接口后，它可以调用接口函数以获取有关子对象的所有对象的描述符。 例如，显示微型端口驱动程序无法提供给拓扑对象的句柄和接口，执行以下步骤来获取拓扑中的所有路径的描述符。

1.  [VidPN 拓扑接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface)

    调用[ *pfnAcquireFirstPathInfo* ](https://msdn.microsoft.com/library/windows/hardware/ff562092) VidPN 拓扑接口，若要获取的指针的函数[ **D3DKMDT\_VIDPN\_存在\_路径**](https://msdn.microsoft.com/library/windows/hardware/ff546647)结构，它描述在拓扑中的第一个路径。

2.  [VidPN 拓扑接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface)

    调用[ *pfnAcquireNextPathInfo* ](https://msdn.microsoft.com/library/windows/hardware/ff562093)重复函数获取指向 D3DKMDT\_VIDPN\_存在\_描述的路径结构拓扑中的其余路径。

同样，显示微型端口驱动程序可以获取描述符的模式，在通过调用设置模式下*pfnAcquireFirstModeInfo*并*pfnAcquireNextModeInfo*的以下模式设置的任何函数接口。

-   [**DXGK\_VIDPNSOURCEMODESET\_INTERFACE**](https://msdn.microsoft.com/library/windows/hardware/ff562073)

-   [**DXGK\_VIDPNTARGETMODESET\_INTERFACE**](https://msdn.microsoft.com/library/windows/hardware/ff562082)

-   [**DXGK\_MONITORSOURCEMODESET\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff561921)

请注意， [ **DXGK\_VIDPNSOURCEMODESET\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff562073)接口中不起源模式集中删除一种模式。 当显示微型端口驱动程序需要更新的源模式集时，它不会更改现有的模式，通过添加和删除模式设置。 相反，它创建一个新的模式集，它取代了旧模式。 必须更新模式集的函数的一个示例是显示微型端口驱动程序[ *DxgkDdiEnumVidPnCofuncModality* ](https://msdn.microsoft.com/library/windows/hardware/ff559649)函数。 更新源模式集的过程中所涉及的步骤如下所示：

1.  调用[ *pfnCreateNewModeInfo* ](https://msdn.microsoft.com/library/windows/hardware/ff562078)的[ **DXGK\_VIDPNSOURCEMODESET\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff562073)接口，用于获取一个指向[ **D3DKMDT\_VIDPN\_源\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff546724) （VidPN 管理器分配） 的结构。

    调用[ *pfnAddMode* ](https://msdn.microsoft.com/library/windows/hardware/ff562077)重复要添加到源模式集的模式。

2.  调用[ *pfnAssignSourceModeSet* ](https://msdn.microsoft.com/library/windows/hardware/ff562840)函数的[ **DXGK\_VIDPN\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff562108)分配新模式设置为特定的视频显示源。 新的源模式集将替换当前分配给该源的源模式集。

更新目标模式集是类似于更新源模式集。 [ **DXGK\_VIDPNTARGETMODESET\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff562082)接口具有以下功能：

-   [VidPN 目标模式设置接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_target_mode)

    一个[ *pfnCreateNewModeInfo* ](https://msdn.microsoft.com/library/windows/hardware/ff562087)函数来创建新的目标模式集和一个[ *pfnAddMode* ](https://msdn.microsoft.com/library/windows/hardware/ff562086)函数添加到集中的模式。

没有任何接口 （函数组），用于获取源和目标属于特定路径。 显示微型端口驱动程序可以确定哪些源和目标属于特定路径通过检查**VidPnSourceId**并**VidPnTargetId**的成员[ **D3DKMDT\_VIDPN\_存在\_路径**](https://msdn.microsoft.com/library/windows/hardware/ff546647)结构，它表示的路径。

## <a name="see-also"></a>请参阅

[确定是否 VidPN 显示适配器上受支持](determining-whether-a-vidpn-is-supported-on-a-display-adapter.md)

[枚举同时正常工作 VidPN 源和目标模式](enumerating-cofunctional-vidpn-source-and-target-modes.md)

[视频存在网络术语](video-present-network-terminology.md)

[获取辅助监视器目标模式](obtaining-additional-monitor-target-modes.md)