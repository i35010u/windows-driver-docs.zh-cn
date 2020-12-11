---
title: 适用于 Windows 10 的驱动程序融合模型
description: 若要使你的设备在 Windows 10 之前的 Windows 和 Windows Phone 版本上工作，你可能需要编写两个独立的驱动程序，一个是 Windows 8.1，一个是 Windows Phone 8.1。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 211fb56c62a77bf18032359b9f1b4878ffcdf504
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828827"
---
# <a name="driver-convergence-model-for-windows-10"></a>适用于 Windows 10 的驱动程序融合模型

若要使你的设备在 Windows 10 之前的 Windows 和 Windows Phone 版本上工作，你可能需要编写两个独立的驱动程序，一个是 Windows 8.1，一个是 Windows Phone 8.1。 在 Windows 10 中，多数情况下，你可以编写一个在任意 Windows 10 版本上运行的驱动程序。 本主题介绍 Windows 10 中设备驱动程序接口的聚合计划，并提供存在版本特定差异情况的详细信息。 其中解答以下问题：

-   对于旧驱动程序，Windows 8.1 驱动程序是否在 Windows 10 桌面版（家庭版、专业版和企业）和/或 Windows 10 移动版上运行？
-   对于新驱动程序，我可以使用 Windows 10 工具包生成一个在 Windows 10 桌面版和 Windows 10 移动版上运行的驱动程序么？

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">技术</th>
<th align="left">Windows 8.1 驱动程序二进制文件是否在 Windows 10 上运行？</th>
<th align="left">Windows 10 的更改</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">音频</td>
<td align="left">是</td>
<td align="left"><p>从 Windows 10 开始，可以为 PnP、电源管理和空闲管理编写调用 KMDF 接口的内核模式驱动程序框架 (KMDF) 音频驱动程序。 对于 I/O 处理，KMDF 音频驱动程序不应使用 WDF 中的 I/O 队列功能，而应使用 PortClass 提供的现有 COM 接口。 但是，驱动程序可以使用计时器、中断、DMA 和远程 I/O 目标的框架支持。 KMDF 音频驱动程序可在 Windows 10 桌面版和 Windows 10 移动版上运行。</p>
<p>链接到 PortClass 的现有 Windows 8.1 驱动程序将继续在 Windows 10 桌面版和 Windows 10 移动版上运行。</p></td>
</tr>
<tr class="even">
<td align="left">生物识别</td>
<td align="left">是</td>
<td align="left"><p>Windows 10 桌面版和 Windows 10 移动版均提供 Windows 生物识别框架 (WBF)。</p>
<p>如果你在为 Windows 10 移动版开发新的生物识别驱动程序，你可以将 Windows 8.1 WBF 驱动程序作为起点。</p></td>
</tr>
<tr class="odd">
<td align="left">Bluetooth</td>
<td align="left">是</td>
<td align="left"><p>在 Windows 10 中，所有设备的蓝牙传输驱动程序接口聚合，并使用通用的蓝牙驱动程序模型。 可以编写在所有 Windows 设备平台上运行的单一驱动程序。</p>
<p>蓝牙音频驱动程序接口区域针对 Windows 10 划分，并允许以下两个选项：</p>
<ul>
<li>可以编写可同时用于桌面设备和移动设备的新的通用音频驱动程序。</li>
<li>现有的 Windows Phone 8.1 蓝牙音频驱动程序将在 Windows 10 移动版上运行。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left">照相机</td>
<td align="left">是</td>
<td align="left"><p>Windows Phone 8.1 中以前提供的功能（如自动对焦和 HFR）在 Windows 10 桌面版和 Windows 10 移动版中均可用。 Windows 8.1 的旧相机驱动程序需要加以修改才能利用这些功能。</p></td>
</tr>
<tr class="odd">
<td align="left">移动电话</td>
<td align="left">是</td>
<td align="left"><p>Windows 10 将继续在电脑上支持数据卡的 MBIM 1.0（移动宽带接口模型）。</p>
<p>使用聚合堆栈等效管理手机网络和 WLAN 连接。 移动运营商可以在 Windows 10 桌面版和 Windows 10 移动版中使用手机网络设置的开放移动联盟设备管理 (OMA DM) 配置。 此外，OEM 将有权访问 Windows 10 桌面版和 Windows 10 移动版中的多变量预配，移动宽带帐户体验 (MBAE) 在 Windows 10 桌面版中仍然可用。</p></td>
</tr>
<tr class="even">
<td align="left">显示器</td>
<td align="left">是</td>
<td align="left"><p>已聚合。 Windows 显示驱动程序模型 (WDDM) 1.3 在 Windows 8.1 和 Windows Phone 8.1 上运行。 WDDM 1.3 继续在 Windows 10 中受支持。 WDDM 2.0 是 Windows 10 的新增功能。 若要使用 Direct3D (D3D) 12 运行时和功能，必须有 WDDM 2.0 驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left">位置</td>
<td align="left">是</td>
<td align="left"><p>适用于 Windows 10 的新全球导航卫星系统 (GNSS) 适配器 DDI。</p>
<p>Windows 8.1 传感器由全球导航卫星系统 (GNSS) 旧 PE 提供支持。</p></td>
</tr>
<tr class="even">
<td align="left">NFC</td>
<td align="left">是</td>
<td align="left"><p>智能卡、无线电收发器管理器、SE 的新 Windows 10 DDI。</p>
<p>Windows 8.1 NFC 驱动程序会继续运行，但无法利用新功能。</p></td>
</tr>
<tr class="odd">
<td align="left">传感器</td>
<td align="left">是</td>
<td align="left"><p>Windows 10 的新驱动程序可以编写用户模式驱动程序框架 (UMDF) 2。使用常见传感器堆栈（类似于 Windows Phone 8.1 模型）的 <em>x</em> 驱动程序与同一驱动程序包在 Windows 10 桌面版和 Windows 10 移动版上运行。</p>
<p>Windows 8.1 传感器类扩展使用 UMDF 1。 Windows Phone 8.1 传感器类扩展使用 UMDF 2。 对于 Windows 10，新传感器类扩展使用 Windows Phone 8.1 这样的 UMDF 2。 若要使用 Windows 10 工具包生成，则必须使用后者。 Windows 8.1 的驱动程序二进制文件仍然在 Windows 10 上运行。 仍然为 Windows 10 内置 HID 类驱动程序，如果你使用 Windows 8.1 已定义的现有 HID 类型，则无需供应商提供的驱动程序和固件更改。</p></td>
</tr>
<tr class="even">
<td align="left">触摸/精确式触摸板 (PTP)</td>
<td align="left">是</td>
<td align="left"><p>在 Windows 10 中，将支持 HID 和触摸微型端口驱动程序。 供应商可以更新旧 HID 驱动程序或实现新的触摸微型端口驱动程序。</p>
<p>对于 Windows 10 移动版，去掉了总线限制，不再限制为 USB、I2C。 当前的类驱动程序保持不变，任何其他总线均需要 HID 微型端口驱动程序。 可以提供支持自定义手势的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left">USB</td>
<td align="left">是</td>
<td align="left"><p>Windows 8.1 提供主控制器堆栈。 Windows 10 添加了允许使用主控制器（电脑/平板电脑/电话）的设备充当外围设备的函数堆栈。</p></td>
</tr>
<tr class="even">
<td align="left">Windows 驱动程序框架 (WDF)</td>
<td align="left">是</td>
<td align="left"><p>Windows 10 附带 KMDF 1.15、UMDF 2.15、UMDF 1.11 和早期的框架版本。 Windows 10 移动版也附带 KMDF 1.15、UMDF 2.15 和早期的框架版本。 请注意，UMDF 版本 1 不在 Windows 10 移动版中提供。 只有 KMDF 和 UMDF 版本 2 可以用来编写 <a href="getting-started-with-windows-drivers.md" data-raw-source="[Windows drivers](getting-started-with-windows-drivers.md)">Windows 驱动程序</a>。</p></td>
</tr>
<tr class="odd">
<td align="left">WLAN</td>
<td align="left">是</td>
<td align="left"><p>WDI（WLAN 设备驱动程序接口）是 Windows 10 新的通用 WLAN 驱动程序模型。 WLAN 设备制造商可以编写在所有设备平台上运行的单个 WDI 微型端口驱动程序，所需要的代码比以前的本机 WLAN 驱动程序模型少。 Windows 10 中引入的所有新 WLAN 功能均需要基于 WDI 的驱动程序。</p>
<p>供应商提供的本机 WLAN 驱动程序继续在 Windows 10 中运行，但功能仅限于开发它们所用于的 Windows 版本。</p></td>
</tr>
</tbody>
</table>

 

 

 





