---
title: WDDM 1.2 和 Windows 8
description: 本部分提供了有关 Windows 显示驱动程序模型中的新功能和增强功能的详细信息 (WDDM) 版本1.2，该版本可从 Windows 8 开始使用。 还介绍了硬件要求、实现准则和使用方案。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20cbc33c379eddd11f77fcd8513d40442aa0ace8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793815"
---
# <a name="wddm-12-and-windows-8"></a>WDDM 1.2 和 Windows 8


本部分提供了有关 Windows 显示驱动程序模型中的新功能和增强功能的详细信息 (WDDM) 版本1.2，该版本可从 Windows 8 开始使用。 还介绍了硬件要求、实现准则和使用方案。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="wddm-v1-2-features.md" data-raw-source="[WDDM 1.2 features](wddm-v1-2-features.md)">WDDM 1.2 功能</a></p></td>
<td align="left"><p>本主题介绍 WDDM 版本1.2 功能集，其中包括一些新的增强功能，这些增强功能可提高性能、可靠性和最终用户体验。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="advances-to-the-display-infrastructure.md" data-raw-source="[Advances to the display Infrastructure](advances-to-the-display-infrastructure.md)">显示基础结构的发展</a></p></td>
<td align="left"><p>Windows 8 为显示基础结构提供了增强功能和优化功能，以进一步改善用户体验。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="direct3d-features-and-requirements.md" data-raw-source="[Direct3D features and requirements in WDDM 1.2](direct3d-features-and-requirements.md)">WDDM 1.2 中的 Direct3D 功能和要求</a></p></td>
<td align="left"><p>Microsoft Direct3D 提供一系列丰富的3-d 图形 Api，软件应用程序广泛使用这些 Api 来实现复杂的可视化和游戏开发。 本部分介绍功能改进以及 Windows 8 Direct3D 软件和硬件要求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="graphics-inf-requirements.md" data-raw-source="[Graphics INF requirements in WDDM 1.2](graphics-inf-requirements.md)">WDDM 1.2 中的图形 INF 要求</a></p></td>
<td align="left"><p>Windows 8 中的 WDDM 驱动程序需要对图形驱动程序进行 INF 更改。 最值得注意的更改是功能分数。 WDDM 1.2 驱动程序需要比早期 WDDM 驱动程序更高的功能分数。 本部分介绍 Windows 8 图形驱动程序的所有相关 INF 要求</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="installation-scenarios.md" data-raw-source="[WDDM 1.2 installation scenarios](installation-scenarios.md)">WDDM 1.2 安装方案</a></p></td>
<td align="left"><p>Windows 8 安装图形驱动程序的行为旨在确保在可能的情况下，我们的客户获得经过 Windows 8 测试和认证的图形驱动程序。 此行为由本部分中描述的规则定义。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wddm-v1-2-driver-enforcement-guidelines.md" data-raw-source="[WDDM 1.2 driver enforcement guidelines](wddm-v1-2-driver-enforcement-guidelines.md)">WDDM 1.2 驱动程序实施指导原则</a></p></td>
<td align="left"><p>本部分介绍 WDDM 1.2 驱动程序强制准则。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idintroductionspanspan-idintroductionspanspan-idintroductionspanintroduction"></a><span id="Introduction"></span><span id="introduction"></span><span id="INTRODUCTION"></span>简介


WDDM 随 Windows Vista 一起引入，作为 Windows XP 或 [windows 2000 显示器驱动程序模型的替换 (XDDM) ](windows-2000-display-driver-model-design-guide.md)。 在 Windows Vista 中，WDDM 体系结构提供了一项功能，可用于启用新功能，如桌面合成、增强的容错、视频内存管理器、GPU 计划程序、Direct3D 表面的跨进程共享等。 WDDM 专门设计用于新式图形设备，这些设备是带有像素着色器2.0 或更高性能的 Microsoft Direct3D 9，具有支持 WDDM 功能所需的所有硬件功能。 WDDM for Windows Vista 称为 "WDDM 1.0"。

Windows 7 对驱动程序模型进行了增量更改，以支持 Windows 7 的特性和功能，并且称为 "WDDM 1.1"。 WDDM 1.1 是 WDDM 1.0 的 strict 超集。 WDDM 1.1 引入了对 Microsoft Direct3D 11、Windows 图形设备接口 (GDI) 硬件加速、连接和配置显示、DirectX 视频加速 (VA) High-Definition (DXVA-HD) 以及许多其他功能的支持。 有关这些功能的详细信息，请参阅 [适用于 Windows 7 的图形指南](/previous-versions/windows/hardware/download/dn550976(v=vs.85))。

Windows 8 引入了一组新特性和功能，需要更改图形驱动程序。 这些增量更改会使最终用户和开发人员受益，并提高系统的可靠性。 启用这些 Windows 8 功能的 WDDM 驱动程序模型称为 "WDDM 1.2"。 WDDM 1.2 是 WDDM 1.1 和 WDDM 1.0 的超集。 这些更改可以用简化形式表示，如下表所示：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">操作系统</th>
<th align="left">支持的驱动程序模型</th>
<th align="left">支持的 Direct3D 版本</th>
<th align="left">启用的功能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Windows Vista</td>
<td align="left">WDDM 1。0
<p>服务器上的 XDDM 和有限 UMPC</p></td>
<td align="left">D3D9、D3D10</td>
<td align="left">计划，内存管理，容错，D3D9 & 10</td>
</tr>
<tr class="even">
<td align="left">Windows Vista SP1/Windows 7 客户端包</td>
<td align="left"><p>WDDM 1.05</p>
<p>服务器2008上的 XDDM</p></td>
<td align="left">D3D9，D3D10，D3D 10。1</td>
<td align="left">+ D3D10 中的 BGRA 支持，D3D 10。1</td>
</tr>
<tr class="odd">
<td align="left">Windows 7</td>
<td align="left"><p>WDDM 1。1</p>
<p>服务器 2008 R2 上的 XDDM</p></td>
<td align="left">D3D9、D3D10、D3D 10.1、D3D11</td>
<td align="left">GDI 硬件加速，DXVA HD，D3D11</td>
</tr>
<tr class="even">
<td align="left">Windows 8</td>
<td align="left">WDDM 1。2</td>
<td align="left">D3D9，D3D10，D3D 10.1，D3D11，D3D 11。1</td>
<td align="left">平滑旋转，Stereoscopic 3-d，D3D11 视频，D3D 11.1，等等。</td>
</tr>
</tbody>
</table>

 

**注意**  
对于 Windows 8 和 WDDM 1.2，不再支持 XDDM，并且 XDDM 驱动程序不会加载到 Windows 8 客户端或服务器上。 对于传统上依赖于 XDDM 的情况，Windows 8 允许迁移到 WDDM，如下表所示。

独立硬件供应商 (Ihv) 和系统构建者应该采用最适合于其客户的其他 WDDM 解决方案。 这意味着，Windows 8 系统将始终具有基于 WDDM 的驱动程序。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">当前正在使用</th>
<th align="left">对 XDDM 方案的 WDDM 支持</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">XDDM VGA 驱动程序</td>
<td align="left">Microsoft 基本显示驱动程序</td>
</tr>
<tr class="even">
<td align="left">XDDM IHV 驱动程序</td>
<td align="left">系统构建者需要使用 IHV 才能获取：
<ul>
<li>Display-Only WDDM 驱动程序或</li>
<li>完整图形 WDDM 驱动程序</li>
</ul>
<p>其他 Microsoft 基本显示器驱动程序</p></td>
</tr>
<tr class="odd">
<td align="left">XDDM 虚拟化驱动程序</td>
<td align="left">系统构建者需要使用 IHV 才能获取新的 Display-Only 虚拟化驱动程序</td>
</tr>
<tr class="even">
<td align="left">适用于 Int10 的 CSM 支持统一可扩展固件接口 (UEFI) </td>
<td align="left">UEFI 图形输出协议不再需要 (GOP) 支持</td>
</tr>
<tr class="odd">
<td align="left">远程桌面访问/Collab</td>
<td align="left">桌面复制 API</td>
</tr>
<tr class="even">
<td align="left">远程会话驱动程序</td>
<td align="left">无更改，不支持 &lt; 32 bpp 模式</td>
</tr>
</tbody>
</table>

 

**注意**  
Microsoft 提供了一个基于 WDDM 的基本显示器驱动程序，该驱动程序是先前的内置 XDDM 标准 VGA 驱动程序的替代，它提供了基本的显示功能以及基于软件的二维和三维呈现方式。

 

WDDM 1.2 引入了新类型的图形驱动程序，面向特定方案，如下所述：

-   **WDDM 完整图形驱动程序：** 这是支持硬件加速二维和三维操作的 WDDM 图形驱动程序的完整版本。 此驱动程序完全能够处理所有渲染、显示和视频功能。 WDDM 1.0 和 WDDM 1.1 是完整的图形驱动程序。 所有 Windows 8 客户端系统都必须具有完整的图形 WDDM 1.2 设备作为主启动设备。
-   **WDDM 仅显示驱动程序**：此驱动程序仅支持作为 WDDM 1.2 驱动程序，并使 ihv 能够编写基于 wddm 的内核模式驱动程序，该驱动程序能够驱动只显示设备。 Windows 使用软件模拟 GPU 处理二维或三维渲染。 仅显示设备不允许作为客户端系统上的主图形设备。
-   **Wddm Render Only 驱动程序**：此驱动程序仅支持作为 WDDM 1.2 驱动程序，并允许 ihv 编写仅支持呈现功能的 WDDM 驱动程序。 仅呈现设备不允许作为客户端系统上的主图形设备。

此表汇总了驱动程序模型与受支持的驱动程序类别：

| 驱动程序型号/驱动程序类别 | 完整图形 | 仅显示 | 仅呈现 |
|------------------------------|---------------|--------------|-------------|
| WDDM 1.0 (Windows Vista)      | 是           | 否           | 否          |
| WDDM 1.1 (Windows 7)          | 是           | 否           | 否          |
| WDDM 1.2 (Windows 8)          | 是           | 是          | 是         |

 

下表说明了新驱动程序类型的方案用法：

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"></th>
<th align="left">客户端</th>
<th align="left">服务器</th>
<th align="left">在虚拟环境中运行的客户端</th>
<th align="left">服务器虚拟</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">完整图形</td>
<td align="left">需要作为启动设备</td>
<td align="left">可选</td>
<td align="left">可选</td>
<td align="left">可选</td>
</tr>
<tr class="even">
<td align="left">Display-Only</td>
<td align="left">不允许</td>
<td align="left">可选</td>
<td align="left">可选</td>
<td align="left">可选</td>
</tr>
<tr class="odd">
<td align="left">Render-Only</td>
<td align="left">可选，作为非主适配器</td>
<td align="left">可选</td>
<td align="left">可选</td>
<td align="left">可选</td>
</tr>
<tr class="even">
<td align="left">外设</td>
<td align="left">不允许</td>
<td align="left">可选</td>
<td align="left">空值</td>
<td align="left">空值</td>
</tr>
</tbody>
</table>

 

Windows 8 随附的所有系统都需要 WDDM 1.2。 WDDM 1.0 和 WDDM 1.1 将继续在 Windows 8 上工作。 但是，仅通过 WDDM 1.2 驱动程序启用最佳体验和 Windows 8 特定功能。

 

