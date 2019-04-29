---
title: WDDM 1.2 和 Windows 8
description: 本部分提供有关新功能和增强功能在 Windows 显示驱动程序模型 (WDDM) 1.2 版的详细信息可从 Windows 8 开始。 它还介绍了硬件要求、 实现指导原则和使用方案。
ms.assetid: 8757ADDD-EDCA-4C09-BB71-2ED925DB2E41
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a2f5b024ef1228b4ccb2fdeb17664a6ffff41f1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391193"
---
# <a name="wddm-12-and-windows-8"></a>WDDM 1.2 和 Windows 8


本部分提供有关新功能和增强功能在 Windows 显示驱动程序模型 (WDDM) 1.2 版的详细信息可从 Windows 8 开始。 它还介绍了硬件要求、 实现指导原则和使用方案。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


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
<td align="left"><p>本主题介绍 WDDM 版本 1.2 功能集，其中包括几个新的增强功能可提高性能、 可靠性和整体最终用户体验。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="advances-to-the-display-infrastructure.md" data-raw-source="[Advances to the display Infrastructure](advances-to-the-display-infrastructure.md)">对显示基础结构的改进</a></p></td>
<td align="left"><p>Windows 8 提供了增强功能并对进一步显示基础结构优化改进用户体验。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="direct3d-features-and-requirements.md" data-raw-source="[Direct3D features and requirements in WDDM 1.2](direct3d-features-and-requirements.md)">Direct3D 功能和 WDDM 1.2 中的要求</a></p></td>
<td align="left"><p>Microsoft Direct3D 提供了一系列丰富的 3-D 图形 Api，广泛使用的软件应用程序以进行复杂的可视化和游戏开发。 本部分介绍功能改进和 Windows 8 Direct3D 软件和硬件要求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="graphics-inf-requirements.md" data-raw-source="[Graphics INF requirements in WDDM 1.2](graphics-inf-requirements.md)">WDDM 1.2 中的图形 INF 要求</a></p></td>
<td align="left"><p>在 Windows 8 中的 WDDM 驱动程序需要图形驱动程序 INF 更改。 最显著的变化是在功能得分。 WDDM 1.2 驱动程序需要较高的功能得分比早期版本的 WDDM 驱动程序。 本部分介绍 Windows 8 图形驱动程序相关的所有 INF 要求</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="installation-scenarios.md" data-raw-source="[WDDM 1.2 installation scenarios](installation-scenarios.md)">WDDM 1.2 安装方案</a></p></td>
<td align="left"><p>Windows 8 安装图形驱动程序行为旨在确保，只要有可能，我们的客户获得的经过测试和针对 Windows 8 认证的图形驱动程序。 此部分所述的规则定义此行为。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wddm-v1-2-driver-enforcement-guidelines.md" data-raw-source="[WDDM 1.2 driver enforcement guidelines](wddm-v1-2-driver-enforcement-guidelines.md)">WDDM 1.2 驱动程序强制实施指南</a></p></td>
<td align="left"><p>本部分介绍 WDDM 1.2 驱动程序强制实施指南。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idintroductionspanspan-idintroductionspanspan-idintroductionspanintroduction"></a><span id="Introduction"></span><span id="introduction"></span><span id="INTRODUCTION"></span>简介


WDDM 引入了 Windows Vista 的 Windows XP 替换或[Windows 2000 显示驱动程序模型 (XDDM)](windows-2000-display-driver-model-design-guide.md)。 通过在 Windows Vista 中引入，WDDM 体系结构提供功能以启用新功能，例如桌面组合、 增强的容错能力、 视频内存管理器、 GPU 计划程序、 跨进程共享的 Direct3D 图面中，依次类推。 WDDM 专门设计为与像素着色器 2.0 或更好，是 Microsoft Direct3D 9 且具有所有必要的硬件功能以支持 WDDM 功能的现代图形设备。 WDDM 适用于 Windows Vista 的称为"WDDM 1.0"。

Windows 7 对增量更改，以支持 Windows 7 的特性和功能的驱动程序模型和称为"WDDM 1.1"。 WDDM 1.1 是 WDDM 1.0 的严格超集。 WDDM 1.1 引入了对 Microsoft Direct3D 11 中，支持 Windows 图形设备接口 (GDI) 硬件加速、 连接和配置显示 DirectX 视频加速 (VA) 高清晰度 (DXVA-HD) 和许多其他功能。 有关这些功能的更多详细信息，请参阅[Windows 7 图形指南](https://go.microsoft.com/fwlink/p/?linkid=327733)。

Windows 8 引入了新特性和功能要求图形驱动程序更改的数组。 这些增量更改中受益的最终用户和开发人员，并提高系统的可靠性。 启用这些 Windows 8 功能的 WDDM 驱动程序模型被称为"WDDM 1.2。" WDDM 1.2 是 WDDM 1.1 和 WDDM 1.0 的超集。 可以在一种简化形式，表示这些更改，此表中所示：

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
<td align="left">WDDM 1.0
<p>服务器和有限的 UMPC 上 XDDM</p></td>
<td align="left">D3D9, D3D10</td>
<td align="left">计划、 内存管理、 容错能力，D3D9 &amp; 10</td>
</tr>
<tr class="even">
<td align="left">Windows Vista SP1 / Windows 7 客户端包</td>
<td align="left"><p>WDDM 1.05</p>
<p>XDDM Server 2008 上</p></td>
<td align="left">D3D9, D3D10, D3D10.1</td>
<td align="left">+ D3D10，D3D 10.1 中 BGRA 支持</td>
</tr>
<tr class="odd">
<td align="left">Windows 7</td>
<td align="left"><p>WDDM 1.1</p>
<p>Server 2008 R2 上的 XDDM</p></td>
<td align="left">D3D9, D3D10, D3D10.1, D3D11</td>
<td align="left">GDI 硬件加速，DXVA HD D3D11</td>
</tr>
<tr class="even">
<td align="left">Windows 8</td>
<td align="left">WDDM 1.2</td>
<td align="left">D3D9, D3D10, D3D10.1, D3D11, D3D11.1</td>
<td align="left">平滑立体三维旋转 D3D11 视频中，D3D11.1，等等。</td>
</tr>
</tbody>
</table>

 

**请注意**  与 Windows 8 和 WDDM 1.2，XDDM 不再受支持，并在 Windows 8 客户端或服务器上不加载 XDDM 驱动程序。 对于传统上依赖于 XDDM 的方案，Windows 8 允许迁移到 WDDM 下一个表中所示。

独立硬件供应商 (Ihv) 和系统构建者应采用替代 WDDM 解决方案最适合他们的客户。 这意味着，Windows 8 系统将始终具有基于 WDDM 驱动程序。

 

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
<td align="left">XDDM VGA Driver</td>
<td align="left">Microsoft 基本显示驱动程序</td>
</tr>
<tr class="even">
<td align="left">XDDM IHV 驱动程序</td>
<td align="left">系统构建者需要使用 IHV 获取：
<ul>
<li>仅显示 WDDM 驱动程序或</li>
<li>所有的图形 WDDM 驱动程序</li>
</ul>
<p>或者 Microsoft 基本显示驱动程序</p></td>
</tr>
<tr class="odd">
<td align="left">XDDM 虚拟化驱动程序</td>
<td align="left">系统构建者需要使用 IHV 以获取新的 Display-Only 虚拟化驱动程序</td>
</tr>
<tr class="even">
<td align="left">CSM Int10 支持上统一可扩展固件接口 (UEFI)</td>
<td align="left">不再需要使用 UEFI 图形输出协议 (GOP) 支持</td>
</tr>
<tr class="odd">
<td align="left">远程桌面访问/协作</td>
<td align="left">桌面复制 API</td>
</tr>
<tr class="even">
<td align="left">远程会话驱动程序</td>
<td align="left">未更改，不支持&lt;32 bpp 模式</td>
</tr>
</tbody>
</table>

 

**请注意**   Microsoft 提供了一个基于 WDDM 的基本显示驱动程序，是前面现成 XDDM 标准 VGA 驱动程序的替代，并提供基本的显示功能和基于软件的二维和三维呈现。

 

WDDM 1.2 引入了新类型的图形驱动程序，面向特定的方案，如下所述：

-   **WDDM 完整图形驱动程序：** 这是支持硬件加速的二维和三维操作 WDDM 图形驱动程序的完整版本。 此驱动程序是完全能够处理所有呈现器、 显示和视频功能。 WDDM 1.0 和 WDDM 1.1 是完整的图形驱动程序。 所有 Windows 8 客户端系统必须都具有完整的图形 WDDM 1.2 设备的主启动设备。
-   **WDDM 显示器仅驱动程序**:此驱动程序为 WDDM 1.2 驱动程序仅支持并启用 Ihv 编写能够推动仅显示设备的 WDDM 基于的内核模式驱动程序。 Windows 通过软件模拟 GPU 处理的二维或三维呈现。 仅显示设备不允许作为客户端系统上的主图形设备。
-   **WDDM 呈现仅驱动程序**:此驱动程序为 WDDM 1.2 驱动程序仅支持并启用 Ihv 编写支持仅呈现功能的 WDDM 驱动程序。 仅限呈现器的设备不允许作为客户端系统上的主图形设备。

下表汇总了与支持的驱动程序类别的驱动程序模型：

| 驱动程序模型/驱动程序类别 | 所有的图形 | 仅显示 | 仅呈现 |
|------------------------------|---------------|--------------|-------------|
| WDDM 1.0 (Windows Vista)     | 是           | 否           | 否          |
| WDDM 1.1 (Windows 7)         | 是           | 否           | 否          |
| WDDM 1.2 (Windows 8)         | 是           | 是          | 是         |

 

下表解释了新的驱动程序类型的方案使用情况：

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
<th align="left">Server</th>
<th align="left">在虚拟环境中运行的客户端</th>
<th align="left">负载均衡器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">所有的图形</td>
<td align="left">所需作为启动设备</td>
<td align="left">可选</td>
<td align="left">可选</td>
<td align="left">可选</td>
</tr>
<tr class="even">
<td align="left">仅显示</td>
<td align="left">不允许</td>
<td align="left">可选</td>
<td align="left">可选</td>
<td align="left">可选</td>
</tr>
<tr class="odd">
<td align="left">仅呈现器</td>
<td align="left">可选选项，因为非主适配器</td>
<td align="left">可选</td>
<td align="left">可选</td>
<td align="left">可选</td>
</tr>
<tr class="even">
<td align="left">无外设</td>
<td align="left">不允许</td>
<td align="left">可选</td>
<td align="left">不可用</td>
<td align="left">不可用</td>
</tr>
</tbody>
</table>

 

WDDM 1.2 是必需的 Windows 8 随附的所有系统。 WDDM 1.0 和 WDDM 1.1 将继续在 Windows 8 上工作。 但是，只能通过 WDDM 1.2 驱动程序启用最佳体验和 Windows 8 特有功能。

 

 





