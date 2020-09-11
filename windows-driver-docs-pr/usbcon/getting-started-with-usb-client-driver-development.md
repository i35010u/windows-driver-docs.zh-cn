---
description: 本部分介绍 USB 驱动程序开发。
title: USB 客户端驱动程序开发的首要步骤
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c07d91f01c928afac323b2e2ae2d74b560d0b64
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010325"
---
# <a name="first-steps-for-usb-client-driver-development"></a>USB 客户端驱动程序开发的首要步骤


本部分介绍 USB 驱动程序开发。 如果你不熟悉驱动程序开发，则该部分适用于你。要实现 USB 设备的驱动程序，Microsoft 不提供内置驱动程序。 此类驱动程序在此文档集中称为 *USB 客户端驱动程序* 。 本节中的主题介绍高级 USB 概念，并提供有关执行 USB 客户端驱动程序的常见任务的分步说明。 有关这些概念的详细信息，请参阅 [Usb 文档](https://go.microsoft.com/fwlink/p/?linkid=617552)中的 usb 规范。

作为驱动程序开发人员，您必须拥有 C 编程语言的编码经验，并了解函数指针、回调函数和事件处理程序的概念。 如果要编写基于用户模式驱动程序框架的驱动程序，请确保熟悉 c + + 和 COM。

## <a name="learning-path-for-usb-client-driver-developers"></a>USB 客户端驱动程序开发人员的学习路径


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>学习步骤</th>
<th>完成该步骤后，你应该能够 .。。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>步骤 1</strong>-阅读 <a href="https://go.microsoft.com/fwlink/p/?linkid=617552" data-raw-source="[Official USB specification version 2.0 and 3.0](https://go.microsoft.com/fwlink/p/?linkid=617552)">官方 USB 规范版本2.0 和 3.0</a>。</p></td>
<td>了解体系结构 (设备、主机控制器和中心) 的行业规范和不同组件。 务必了解数据流模型，主机和设备之间如何相互通信，以及设备所需的请求格式。</td>
</tr>
<tr class="even">
<td><p><strong>步骤 2</strong>-获取测试 USB 设备。</p></td>
<td><ul>
<li>具有 USB 设备及其硬件规范。 该规范描述了设备功能和支持的供应商命令。 使用规范来确定设备驱动程序的功能以及相关的设计决策。</li>
<li>如果你不熟悉 USB 驱动程序开发，请使用 OSR USB FX2 学习工具包。 此工具包最适合学习本文档集中包括的 USB 示例。 可以从 <a href="https://go.microsoft.com/fwlink/p/?linkid=617553" data-raw-source="[OSR Online](https://go.microsoft.com/fwlink/p/?linkid=617553)">OSR Online</a>获取学习工具包。</li>
<li>使用 Microsoft USB 测试工具 (MUTT) 设备。 可以从 <a href="https://go.microsoft.com/fwlink/p/?linkid=617554" data-raw-source="[JJG Technologies](https://go.microsoft.com/fwlink/p/?linkid=617554)">JJG 技术</a>购买 MUTT 硬件。 设备未安装安装的固件。 若要安装固件，请 <a href="https://go.microsoft.com/fwlink/p/?linkid=617555" data-raw-source="[download the MUTT software package](https://go.microsoft.com/fwlink/p/?linkid=617555)">下载 MUTT</a>软件包，并运行 MUTTUtil.exe。 有关详细信息，请参阅包附带的文档。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>步骤 3</strong>-研究 <a href="usb-device-layout.md" data-raw-source="[USB device layout](usb-device-layout.md)">usb 设备布局</a> 和相关 <a href="usb-descriptors.md" data-raw-source="[USB descriptors](usb-descriptors.md)">usb 描述符</a>。</p></td>
<td>通过阅读配置描述符、每个受支持的备用设置的接口描述符及其终结点描述符来描述你的设备功能。 通过使用 <a href="https://go.microsoft.com/fwlink/p/?linkid=617556" data-raw-source="[USBView](https://go.microsoft.com/fwlink/p/?linkid=617556)">USBView</a>，你可以浏览所有 usb 控制器和连接到它们的 usb 设备，还可以检查设备配置。</td>
</tr>
<tr class="even">
<td><p><strong>步骤 4</strong>-<a href="winusb-considerations.md" data-raw-source="[Choose a driver model for developing a USB client driver](winusb-considerations.md)">选择用于开发 USB 客户端驱动程序的驱动程序模型</a>。</p></td>
<td>根据设备的设计，确定是编写自定义驱动程序还是使用 Microsoft 提供的驱动程序之一。 若要编写驱动程序，请选择最佳驱动程序模型并描述每个模型支持的功能。</td>
</tr>
<tr class="odd">
<td><p><strong>步骤 5</strong>-熟悉 Microsoft 提供的 USB 驱动程序堆栈和驱动程序开发概念。</p>
<ul>
<li><a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers in Windows](usb-3-0-driver-stack-architecture.md)">Windows 中的 USB 宿主端驱动程序</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers" data-raw-source="[Concepts for All Driver Developers](../gettingstarted/concepts-and-knowledge-for-all-driver-developers.md)">适用于所有驱动程序开发人员的概念</a></li>
<li><a href="usb-concepts-for-all-developers.md" data-raw-source="[Concepts for all USB developers](usb-concepts-for-all-developers.md)">适用于所有 USB 开发人员的概念</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/device-nodes-and-device-stacks" data-raw-source="[Device nodes and device stacks](../gettingstarted/device-nodes-and-device-stacks.md)">设备节点和设备堆栈</a></li>
<li><em>使用 Windows Driver Foundation 开发驱动程序</em>，由 "Orwick" 和 "专家 Smith" 编写。 有关详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/developing-drivers-with-wdf" data-raw-source="[Developing Drivers with WDF](../wdf/developing-drivers-with-wdf.md)">通过 WDF 开发驱动程序</a>。</li>
<li><a href="usb-driver-samples-in-wdk.md" data-raw-source="[USB driver samples](usb-driver-samples-in-wdk.md)">USB 驱动程序示例</a></li>
</ul></td>
<td><ul>
<li>了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助您做出适当的设计决策，并使您能够简化开发过程。</li>
<li>区分用户模式和内核模式驱动程序体系结构模型。</li>
<li>了解驱动程序加载以及 Windows 如何在设备树和设备节点中组织即插即用 (PnP) 设备。 你还应了解 PnP 管理器如何生成设备堆栈以及你的驱动程序及其设备对象放置在设备堆栈中的位置。</li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>步骤 6</strong>-准备开发和调试环境。</p>
<ul>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=617580" data-raw-source="[Install the latest Windows Driver Kit (WDK)](https://go.microsoft.com/fwlink/p/?linkid=617580)"> (WDK) 安装最新的 Windows 驱动程序工具包 </a>。</li>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=617580" data-raw-source="[Install Microsoft Visual Studio 2012](https://go.microsoft.com/fwlink/p/?linkid=617580)">安装 2012 Microsoft Visual Studio</a>。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/getting-set-up-for-debugging" data-raw-source="[Get Set Up for Debugging](../debugger/getting-set-up-for-debugging.md)">设置以进行调试</a>。</li>
<li>请确保具有 <a href="headers-and-libraries-for-a-usb-client-driver.md" data-raw-source="[Headers and libraries required by a USB client driver](headers-and-libraries-for-a-usb-client-driver.md)">USB 客户端驱动程序所需的标头和库</a>。</li>
</ul></td>
<td><ul>
<li>如果要编写内核模式驱动程序，应在主机和目标计算机上通过以太网网络、1394电缆、USB 2.0 或3.0 调试电缆或空调缆线配置调试。</li>
<li>如果要编写用户模式驱动程序，可以使用 Microsoft Visual Studio 环境中可用的用户模式调试器。 你应该知道 <a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/debugging-a-user-mode-process-using-visual-studio" data-raw-source="[how to attach to a process or launch a process under the debugger](../debugger/debugging-a-user-mode-process-using-visual-studio.md)">如何附加到进程或在调试器下启动进程</a>。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>步骤 7</strong>—编写你的第一个驱动程序。</p>
<ul>
<li><a href="tutorial--write-your-first-usb-client-driver--kmdf-.md" data-raw-source="[How to write your first USB client driver (KMDF)](tutorial--write-your-first-usb-client-driver--kmdf-.md)">如何编写第一个 USB 客户端驱动程序 (KMDF)</a></li>
<li><a href="implement-driver-entry-for-a-usb-driver--umdf-.md" data-raw-source="[How to write your first USB client driver (UMDF)](implement-driver-entry-for-a-usb-driver--umdf-.md)">如何编写第一个 USB 客户端驱动程序 (UMDF)</a></li>
</ul></td>
<td>使用 Visual Studio 2012 附带的 USB 模板，编写、生成和安装第一个 USB 客户端驱动程序。 应该能够描述框架驱动程序、设备和队列对象，并了解框架如何与驱动程序通信。</td>
</tr>
<tr class="even">
<td><strong>步骤 8</strong>-通过发送 USB 控制传输请求来扩展驱动程序。</td>
<td>将标准控制请求和供应商命令发送到设备。 有关详细信息，请参阅 <a href="usb-control-transfer.md" data-raw-source="[How to send a USB control transfer](usb-control-transfer.md)">如何发送 USB 控件传输</a>。</td>
</tr>
<tr class="odd">
<td><p><strong>步骤 9</strong>-扩展驱动程序，使用 WDF usb i/o 目标对象执行 USB 数据传输。 <a href="usb-device-i-o.md" data-raw-source="[USB data transfers](usb-device-i-o.md)">USB 数据传输</a>。</p></td>
<td><p>扩展驱动程序以执行常见任务。 本主题列出了本文档集中的 "如何" 主题，其中提供了有关这些任务的分步指导。</p>
<ul>
<li><a href="wdk-resources-for-usb-driver-development.md" data-raw-source="[Common tasks for USB client drivers](wdk-resources-for-usb-driver-development.md)">USB 客户端驱动程序的常见任务</a></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="community-resources-for-usb"></a>用于 USB 的社区资源


<a href="" id="microsoft-windows-usb-core-team-blog"></a>[Microsoft Windows USB 核心团队博客](https://go.microsoft.com/fwlink/p/?linkid=617581)  
查看 Microsoft USB 团队撰写的博文。 此博客重点介绍 Windows USB 驱动程序堆栈，该堆栈适用于 Windows 电脑中的各种 USB 主控制器和 USB 集线器。 适用于 USB 客户端驱动程序开发人员和 USB 硬件设计人员的资源，方便他们了解驱动程序堆栈实现、解决常见问题以及如何使用工具来收集跟踪和日志文件。

<a href="" id="osr-online-lists---ntdev"></a>[OSR Online 列表-ntdev](https://go.microsoft.com/fwlink/p/?linkid=617582)  
由 [OSR Online](https://go.microsoft.com/fwlink/p/?linkid=617590) 管理的讨论列表，适用于内核模式驱动程序开发人员。

<a href="" id="usb-technologies"></a>[USB 技术](https://go.microsoft.com/fwlink/p/?linkid=617583)  
各种基于常见问题的资源，这些问题由不熟悉 Windows 操作系统的 USB 设备和驱动程序开发的开发人员提出。

<a href="" id="windows-dev-center-for-hardware-development"></a>[用于硬件开发的 Windows 开发人员中心](https://go.microsoft.com/fwlink/p/?linkid=617584)  
[下载用于驱动程序开发的最新工具](https://go.microsoft.com/fwlink/p/?linkid=617585)，通过 [windows 认证计划](https://go.microsoft.com/fwlink/p/?linkid=617591)确保你的产品可靠且与 windows 兼容，并了解 [windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)。

## <a name="related-topics"></a>相关主题
[ (USB) 驱动程序的通用串行总线](../index.yml)  
[如何在 USB 设备的 UMDF 驱动程序中启用 USB 选择性挂起和系统唤醒](https://go.microsoft.com/fwlink/p/?linkid=617587)  
[USB 驱动程序开发指南](usb-driver-development-guide.md)