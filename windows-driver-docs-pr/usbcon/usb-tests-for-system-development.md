---
Description: 如果要生成一个新系统，建议使用本主题中的测试。
title: 建议用于系统开发的 USB 测试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25a1885bb0b2f3b60c4eb163e01dec18a9a52aa6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356575"
---
# <a name="recommended-usb-tests-for-system-development"></a>建议用于系统开发的 USB 测试


如果要生成一个新系统，建议使用本主题中的测试。

若要运行本主题中列出的 DF 测试，必须具有[MUTT 设备](microsoft-usb-test-tool--mutt--devices.md)。 具体取决于该阶段，需要通过运行以下命令更新该设备驱动程序：

`muttutil -updatedriver <driver_inf>.inf`

[MuttUtil](muttutil.md)工具包含在[MUTT 软件包](mutt-software-package.md)。

如果要生成一个新系统，下面是推荐的 USB HCK 测试：

## <a name="stage-1system-bring-up"></a>阶段 1 — 系统启动


-   [DF-IO （基本） 前后的睡眠](https://docs.microsoft.com/previous-versions/windows/hardware/hck/dn247481(v=vs.85))
-   [DF - PNP（禁用和启用），带 IO 之前和之后（基本）](https://docs.microsoft.com/previous-versions/windows/hardware/hck/dn260411(v=vs.85))
-   [USB 公开端口测试控制器](https://docs.microsoft.com/previous-versions/windows/hardware/hck/hh998021(v=vs.85))
-   [USB xHCI 传输速度测试](https://docs.microsoft.com/previous-versions/windows/hardware/hck/hh997864(v=vs.85))
-   [USB3 终止](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124672(v=vs.85))

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>对于每个 xHCI 控制器在系统上，配置此拓扑</th>
<th>运行建议的测试</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ol>
<li>连接到系统的 SuperSpeed 端口 USB 3.0 集线器。</li>
<li><p>连接 USB 3.0 集线器的 SuperMUTT 下游。</p>
<p></p>
<p><strong>设备驱动程序：  </strong>SuperMUTT 设备必须具有 Winusb.sys 作为设备驱动程序。 运行此命令：</p>
<p><code>muttutil -updatedriver usbfx2.inf</code></p>
<p><img src="images/xhci-superspeedhub-supermutt.png" alt="System bring-up topology" /></p></li>
</ol>
<div class="alert">
<strong>请注意</strong>  如果系统不具有类型的连接器，则适配器应将与系统包括在内。
</div>
<div>
 
</div></td>
<td><ol>
<li>在 Windows HCK Studio 中，在<strong>选定内容</strong>选项卡上，单击<strong>设备管理器</strong>。</li>
<li>选择 xHCI 控制器和其根集线器。
<div class="alert">
<strong>请注意</strong>  要快速查找控制器，请在搜索中键入"xhci"。
</div>
<div>
 
</div></li>
<li>从<strong>视图通过</strong>列表中，选择<strong>基本</strong>。</li>
<li>运行建议的用于所选的控制器。</li>
</ol></td>
</tr>
</tbody>
</table>

 

## <a name="stage-2system-integration"></a>阶段 2-系统集成


-   [DF-重启为重新启动 IO 之前和之后 （功能）](https://docs.microsoft.com/previous-versions/windows/hardware/hck/dn260266(v=vs.85))
-   [DF-睡眠和 PNP （禁用和启用） IO 前后的 （功能）](https://docs.microsoft.com/previous-versions/windows/hardware/hck/dn260391(v=vs.85))
-   [USB xHCI 传输速度测试](https://docs.microsoft.com/previous-versions/windows/hardware/hck/hh997864(v=vs.85))

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>对于每个 xHCI 控制器在系统上，配置此拓扑</th>
<th>运行建议的测试</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p>
<p>对于每个 xHCI 控制器在系统上，配置此拓扑</p>
<ol>
<li>连接到系统的 SuperSpeed 端口 USB 3.0 集线器。</li>
<li><p>连接 USB 3.0 集线器的 SuperMUTT 下游。</p>
<p><strong>设备驱动程序：  </strong>SuperMUTT 设备必须具有 Usbtcd.sys 作为设备驱动程序。 运行此命令：</p>
<p><code>muttutil -updatedriver usbtcd.inf</code></p></li>
<li>SuperMUTT 包下游的 USB 3.0 集线器连接。</li>
</ol>
<p><img src="images/xhci-system-integration.png" alt="System integration topology" /></p>
<p></p>
<div class="alert">
<strong>请注意</strong>  如果系统不具有类型的连接器，则适配器应将与系统包括在内。
</div>
<div>
 
</div></td>
<td><p>若要运行测试：</p>
<ol>
<li>上<strong>选定内容</strong>选项卡上，单击<strong>设备管理器</strong>。</li>
<li>选择 xHCI 控制器和其根集线器。
<div class="alert">
<strong>请注意</strong>  要快速查找控制器，请在搜索中键入"xhci"。
</div>
<div>
 
</div></li>
<li>从<strong>视图通过</strong>列表中，选择<strong>功能</strong>。</li>
<li>运行建议的用于所选的控制器。</li>
</ol></td>
</tr>
</tbody>
</table>

 

## <a name="stage-3system-tuneup"></a>第 3 阶段-系统调整


系统 1

-   [DF-睡眠 （认证） 期间的 IO](https://docs.microsoft.com/previous-versions/windows/hardware/hck/dn247416(v=vs.85))
-   [DF-并发硬件和操作系统系统 (CHAOS) 测试 （认证）](https://docs.microsoft.com/previous-versions/windows/hardware/hck/hh998603(v=vs.85))

系统 2

-   [DF-睡眠和 PNP （禁用和启用） IO 前后的 （功能）](https://docs.microsoft.com/previous-versions/windows/hardware/hck/dn260391(v=vs.85))
-   [USB xHCI 传输速度测试](https://docs.microsoft.com/previous-versions/windows/hardware/hck/hh997864(v=vs.85))

系统 3 （如果停靠支持）

-   运行测试的列出[系统集成阶段](#stage-2system-integration)停靠的系统上。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>对于每个 xHCI 控制器在系统上，配置此拓扑</th>
<th>运行建议的测试</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>系统 1</p>
<p>请参阅<a href="#stage-1system-bring-up" data-raw-source="[system bring-up topology](#stage-1system-bring-up)">系统启动拓扑</a>。</p>
<p><strong>设备驱动程序：  </strong>SuperMUTT 设备必须具有 Usbtcd.sys 作为设备驱动程序。 运行此命令：</p>
<p><code>muttutil -updatedriver usbtcd.inf</code></p>
<p>系统 2</p>
<p>对于每个 xHCI 控制器在系统上，配置此拓扑</p>
<ol>
<li>连接到系统的 SuperSpeed 端口 USB 3.0 集线器。</li>
<li>连接 USB 3.0 集线器的 SuperMUTT 下游。</li>
<li>SuperMUTT 包下游的 USB 3.0 集线器连接。</li>
<li>MUTT 包下游的 USB 3.0 集线器连接。</li>
<li>连接四个自供电的 USB 3.0 集线器下游的每个其他 （构成链） 使用 SuperMUTT 包的第一个下游的中心。</li>
<li>连接 MUTT （或 SuperMUTT 包） 的最后一个 USB 3.0 集线器链中下一级。</li>
</ol>
<img src="images/xhci-superspeedhub-hub-daisy.png" alt="System tuning topology" />
<p>系统 3 （如果停靠支持）</p>
<p>请参阅<a href="#stage-2system-integration" data-raw-source="[system integration stage](#stage-2system-integration)">系统集成阶段</a>。</p></td>
<td><p>系统 1</p>
<ol>
<li>上<strong>选定内容</strong>选项卡上，单击<strong>设备管理器</strong>。</li>
<li>选择 xHCI 控制器和其根集线器。
<div class="alert">
<strong>请注意</strong>  要快速查找控制器，请在搜索中键入"xhci"。
</div>
<div>
 
</div></li>
<li>从<strong>视图通过</strong>列表中，选择<strong>认证</strong>。</li>
<li>运行建议的用于所选的控制器。</li>
</ol>
<p>系统 2</p>
<ol>
<li>上<strong>选定内容</strong>选项卡上，单击<strong>设备管理器</strong>。</li>
<li>在拓扑中，显示在列表中选择所有 MUTT 设备。
<div class="alert">
<strong>请注意</strong>  要快速查找控制器，请在搜索中键入"MUTT"。
</div>
<div>
 
</div></li>
<li>从<strong>视图通过</strong>列表中，选择<strong>功能</strong>。</li>
<li>运行系统 2 推荐的测试。</li>
<li>使用 2 米长电缆连接到系统的中心。</li>
</ol>
<p>系统 3</p>
<ul>
<li><p>与相同<a href="#stage-2system-integration" data-raw-source="[system integration topology](#stage-2system-integration)">系统集成拓扑</a>。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[有关 USB 的 Windows 硬件实验室工具包测试](windows-hardware-certification-kit-tests-for-usb.md)  



