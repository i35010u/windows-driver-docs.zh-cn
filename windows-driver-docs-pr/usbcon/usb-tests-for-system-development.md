---
description: 如果要构建新系统，则建议使用本主题中的测试。
title: 建议用于系统开发的 USB 测试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dddfbfee24592d8a637ccc520c9290fd74638ff3
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968596"
---
# <a name="recommended-usb-tests-for-system-development"></a>建议用于系统开发的 USB 测试


如果要构建新系统，则建议使用本主题中的测试。

若要运行本主题中列出的 DF 测试，则必须具有 [MUTT 设备](microsoft-usb-test-tool--mutt--devices.md)。 根据阶段，你将需要通过运行以下命令来更新设备的驱动程序：

`muttutil -updatedriver <driver_inf>.inf`

[MuttUtil](muttutil.md)工具包含在[MUTT](mutt-software-package.md)软件包中。

如果要构建新系统，建议使用以下 USB HCK 测试：

## <a name="stage-1system-bring-up"></a>阶段 1-系统启动


-   [DF –在 (基本) 之前和之后休眠 ](https://docs.microsoft.com/previous-versions/windows/hardware/hck/dn247481(v=vs.85))
-   [DF - PNP（禁用和启用），带 IO 之前和之后（基本）](https://docs.microsoft.com/previous-versions/windows/hardware/hck/dn260411(v=vs.85))
-   [USB 公开端口控制器测试](https://docs.microsoft.com/previous-versions/windows/hardware/hck/hh998021(v=vs.85))
-   [USB xHCI 传输速度测试](https://docs.microsoft.com/previous-versions/windows/hardware/hck/hh997864(v=vs.85))
-   [USB3 终止](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124672(v=vs.85))

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>对于系统上的每个 xHCI 控制器，配置此拓扑</th>
<th>运行建议的测试</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ol>
<li>将 USB 3.0 集线器连接到系统的 SuperSpeed 端口。</li>
<li><p>连接 USB 3.0 集线器的 SuperMUTT 下游。</p>
<p></p>
<p><strong>设备驱动程序：  </strong>SuperMUTT 设备的设备驱动程序必须 Winusb.sys。 运行以下命令：</p>
<p><code>muttutil -updatedriver usbfx2.inf</code></p>
<p><img src="images/xhci-superspeedhub-supermutt.png" alt="System bring-up topology" /></p></li>
</ol>
<div class="alert">
<strong>注意</strong>   如果系统没有连接器类型，则应将适配器包含在系统中。
</div>
<div>
 
</div></td>
<td><ol>
<li>在 Windows HCK Studio 中的 " <strong>选择</strong> " 选项卡上，单击 " <strong>设备管理器</strong>"。</li>
<li>选择 xHCI 控制器及其根集线器。
<div class="alert">
<strong>注意</strong>   若要快速查找控制器，请在 "搜索" 中键入 "xhci"。
</div>
<div>
 
</div></li>
<li>从 " <strong>查看方式</strong> " 列表中，选择 " <strong>基本</strong>"。</li>
<li>为所选控制器运行建议的。</li>
</ol></td>
</tr>
</tbody>
</table>

 

## <a name="stage-2system-integration"></a>阶段 2-系统集成


-   [DF-在 (功能之前和之后，重启和 IO 重启) ](https://docs.microsoft.com/previous-versions/windows/hardware/hck/dn260266(v=vs.85))
-   [DF-睡眠和 PNP (禁用和启用 (功能之前和之后的 IO) ) ](https://docs.microsoft.com/previous-versions/windows/hardware/hck/dn260391(v=vs.85))
-   [USB xHCI 传输速度测试](https://docs.microsoft.com/previous-versions/windows/hardware/hck/hh997864(v=vs.85))

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>对于系统上的每个 xHCI 控制器，配置此拓扑</th>
<th>运行建议的测试</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p>
<p>对于系统上的每个 xHCI 控制器，配置此拓扑</p>
<ol>
<li>将 USB 3.0 集线器连接到系统的 SuperSpeed 端口。</li>
<li><p>连接 USB 3.0 集线器的 SuperMUTT 下游。</p>
<p><strong>设备驱动程序：  </strong>SuperMUTT 设备的设备驱动程序必须 Usbtcd.sys。 运行以下命令：</p>
<p><code>muttutil -updatedriver usbtcd.inf</code></p></li>
<li>连接 USB 3.0 集线器的下游 SuperMUTT 包。</li>
</ol>
<p><img src="images/xhci-system-integration.png" alt="System integration topology" /></p>
<p></p>
<div class="alert">
<strong>注意</strong>   如果系统没有连接器类型，则应将适配器包含在系统中。
</div>
<div>
 
</div></td>
<td><p>运行测试：</p>
<ol>
<li>在 " <strong>选择</strong> " 选项卡上，单击 " <strong>设备管理器</strong>"。</li>
<li>选择 xHCI 控制器及其根集线器。
<div class="alert">
<strong>注意</strong>   若要快速查找控制器，请在 "搜索" 中键入 "xhci"。
</div>
<div>
 
</div></li>
<li>从 " <strong>查看方式</strong> " 列表中，选择 " <strong>功能</strong>"。</li>
<li>为所选控制器运行建议的。</li>
</ol></td>
</tr>
</tbody>
</table>

 

## <a name="stage-3system-tuneup"></a>阶段3—系统调准


系统1

-   [DF- (认证期间休眠 IO) ](https://docs.microsoft.com/previous-versions/windows/hardware/hck/dn247416(v=vs.85))
-   [DF-并发硬件和操作系统 (混乱) 测试 (认证) ](https://docs.microsoft.com/previous-versions/windows/hardware/hck/hh998603(v=vs.85))

系统2

-   [DF-睡眠和 PNP (禁用和启用 (功能之前和之后的 IO) ) ](https://docs.microsoft.com/previous-versions/windows/hardware/hck/dn260391(v=vs.85))
-   [USB xHCI 传输速度测试](https://docs.microsoft.com/previous-versions/windows/hardware/hck/hh997864(v=vs.85))

系统 3 (如果支持 dock) 

-   在停靠系统上运行 [系统集成阶段](#stage-2system-integration) 列出的测试。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>对于系统上的每个 xHCI 控制器，配置此拓扑</th>
<th>运行建议的测试</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>系统1</p>
<p>请参阅 <a href="#stage-1system-bring-up" data-raw-source="[system bring-up topology](#stage-1system-bring-up)">系统启动拓扑</a>。</p>
<p><strong>设备驱动程序：  </strong>SuperMUTT 设备的设备驱动程序必须 Usbtcd.sys。 运行以下命令：</p>
<p><code>muttutil -updatedriver usbtcd.inf</code></p>
<p>系统2</p>
<p>对于系统上的每个 xHCI 控制器，配置此拓扑</p>
<ol>
<li>将 USB 3.0 集线器连接到系统的 SuperSpeed 端口。</li>
<li>连接 USB 3.0 集线器的 SuperMUTT 下游。</li>
<li>连接 USB 3.0 集线器的下游 SuperMUTT 包。</li>
<li>连接 USB 3.0 集线器的下游 MUTT 包。</li>
<li>将四个自驱动的 USB 3.0 中心彼此下游连接 (形成与 SuperMUTT Pack 的第一个集线器下游) 的链。</li>
<li>将 MUTT (或 SuperMUTT) Pack 连接到链中最后一个 USB 3.0 集线器的下游。</li>
</ol>
<img src="images/xhci-superspeedhub-hub-daisy.png" alt="System tuning topology" />
<p>系统 3 (如果支持 dock) </p>
<p>请参阅 <a href="#stage-2system-integration" data-raw-source="[system integration stage](#stage-2system-integration)">系统集成阶段</a>。</p></td>
<td><p>系统1</p>
<ol>
<li>在 " <strong>选择</strong> " 选项卡上，单击 " <strong>设备管理器</strong>"。</li>
<li>选择 xHCI 控制器及其根集线器。
<div class="alert">
<strong>注意</strong>   若要快速查找控制器，请在 "搜索" 中键入 "xhci"。
</div>
<div>
 
</div></li>
<li>从 " <strong>查看方式</strong> " 列表中，选择 " <strong>认证</strong>"。</li>
<li>为所选控制器运行建议的。</li>
</ol>
<p>系统2</p>
<ol>
<li>在 " <strong>选择</strong> " 选项卡上，单击 " <strong>设备管理器</strong>"。</li>
<li>选择拓扑中的所有 MUTT 设备，显示在列表中。
<div class="alert">
<strong>注意</strong>   若要快速查找控制器，请在 "搜索" 中键入 "MUTT"。
</div>
<div>
 
</div></li>
<li>从 " <strong>查看方式</strong> " 列表中，选择 " <strong>功能</strong>"。</li>
<li>为系统2运行建议的测试。</li>
<li>使用2米长电缆将集线器连接到系统。</li>
</ol>
<p>系统3</p>
<ul>
<li><p>与 <a href="#stage-2system-integration" data-raw-source="[system integration topology](#stage-2system-integration)">系统集成拓扑</a>相同。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[适用于 USB 的 Windows 硬件实验室包测试](windows-hardware-certification-kit-tests-for-usb.md)  



