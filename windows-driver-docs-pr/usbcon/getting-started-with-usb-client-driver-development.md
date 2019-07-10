---
Description: 本部分介绍 USB 驱动程序开发。
title: USB 客户端驱动程序开发的第一个步骤
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fdd6588651943e01b3215d26b89ac564a475655
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716967"
---
# <a name="first-steps-for-usb-client-driver-development"></a>USB 客户端驱动程序开发的第一个步骤


本部分介绍 USB 驱动程序开发。 如果您不熟悉驱动程序开发; 部分适用于您想要实现 USB 设备，Microsoft 不提供现成驱动程序的驱动程序。 此类驱动程序称为*USB 客户端驱动程序*本文档中设置。 在本部分中的主题介绍高级 USB 概念并提供有关执行常见任务的 USB 客户端驱动程序的分步说明。 有关这些概念的详细信息，请参阅上的 USB 规范[USB 文档](https://go.microsoft.com/fwlink/p/?linkid=617552)。

驱动程序开发人员必须有编码经验，在 C 编程语言中，并了解函数指针、 回调函数和事件处理程序的概念。 如果要编写驱动程序基于用户模式驱动程序框架，请确保使自己熟悉C++和 com。

## <a name="learning-path-for-usb-client-driver-developers"></a>USB 客户端驱动程序开发人员的学习路径


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>学习步骤</th>
<th>完成步骤后，您应能...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>步骤 1</strong>— 阅读<a href="https://go.microsoft.com/fwlink/p/?linkid=617552" data-raw-source="[Official USB specification version 2.0 and 3.0](https://go.microsoft.com/fwlink/p/?linkid=617552)">官方 USB 2.0 和 3.0 规范版本</a>。</p></td>
<td>了解行业规范和体系结构的不同组件 （设备、 主控制器和中心）。 务必了解数据流模型，与每个其他和的设备需要请求格式的通信的主机和设备的方式。</td>
</tr>
<tr class="even">
<td><p><strong>步骤 2</strong>— 获取测试 USB 设备。</p></td>
<td><ul>
<li>具有 USB 设备和其硬件规范。 此规范描述设备功能和受支持的供应商命令。 使用规范来确定设备驱动程序和相关的设计决策的功能。</li>
<li>如果您不熟悉 USB 驱动程序开发，具有 OSR USB FX2 学习工具包。 此工具包最适合学习本文档集中包括的 USB 示例。 就可以从学习工具包<a href="https://go.microsoft.com/fwlink/p/?linkid=617553" data-raw-source="[OSR Online](https://go.microsoft.com/fwlink/p/?linkid=617553)">OSR 联机</a>。</li>
<li>拥有 Microsoft USB 测试工具 (MUTT) 设备。 可以从购买 MUTT 硬件<a href="https://go.microsoft.com/fwlink/p/?linkid=617554" data-raw-source="[JJG Technologies](https://go.microsoft.com/fwlink/p/?linkid=617554)">JJG 技术</a>。 设备没有安装的已安装的固件。 若要安装固件<a href="https://go.microsoft.com/fwlink/p/?linkid=617555" data-raw-source="[download the MUTT software package](https://go.microsoft.com/fwlink/p/?linkid=617555)">下载 MUTT 软件包</a>，并运行 MUTTUtil.exe。 有关详细信息，请参阅随程序包提供的文档。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>步骤 3</strong>— 研究您<a href="usb-device-layout.md" data-raw-source="[USB device layout](usb-device-layout.md)">USB 设备布局</a>以及相关<a href="usb-descriptors.md" data-raw-source="[USB descriptors](usb-descriptors.md)">USB 描述符</a>。</p></td>
<td>通过阅读配置描述符，接口描述符的每个受支持的替代设置，并将其终结点描述符来描述你设备的功能。 通过使用<a href="https://go.microsoft.com/fwlink/p/?linkid=617556" data-raw-source="[USBView](https://go.microsoft.com/fwlink/p/?linkid=617556)">USBView</a>，可以浏览所有 USB 控制器和 USB 设备连接到它们，并还检查设备配置。</td>
</tr>
<tr class="even">
<td><p><strong>步骤 4</strong>—<a href="winusb-considerations.md" data-raw-source="[Choose a driver model for developing a USB client driver](winusb-considerations.md)">选择用于开发 USB 客户端驱动程序的驱动程序模型</a>。</p></td>
<td>确定是否应编写自定义驱动程序或使用基于设备的设计的 Microsoft 提供的驱动因素之一。 对于编写的驱动程序，选择最佳的驱动程序模型并描述每个模型支持的功能。</td>
</tr>
<tr class="odd">
<td><p><strong>步骤 5</strong>— 你熟悉 Microsoft 提供的 USB 驱动程序堆栈和驱动程序开发概念。</p>
<ul>
<li><a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers in Windows](usb-3-0-driver-stack-architecture.md)">在 Windows 中的 USB 宿主端驱动程序</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers" data-raw-source="[Concepts for All Driver Developers](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)">对所有驱动程序开发人员概念</a></li>
<li><a href="usb-concepts-for-all-developers.md" data-raw-source="[Concepts for all USB developers](usb-concepts-for-all-developers.md)">所有 USB 开发人员的概念</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/device-nodes-and-device-stacks" data-raw-source="[Device nodes and device stacks](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/device-nodes-and-device-stacks)">设备节点和设备堆栈</a></li>
<li><em>使用 Windows Driver Foundation 开发驱动程序</em>、 由 Penny Orwick 和 Smith 专家编写。 有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/developing-drivers-with-wdf" data-raw-source="[Developing Drivers with WDF](https://docs.microsoft.com/windows-hardware/drivers/wdf/developing-drivers-with-wdf)">开发驱动程序与 WDF</a>。</li>
<li><a href="usb-driver-samples-in-wdk.md" data-raw-source="[USB driver samples](usb-driver-samples-in-wdk.md)">USB 驱动程序示例</a></li>
</ul></td>
<td><ul>
<li>了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助您做出适当的设计决策，并可用于简化开发过程。</li>
<li>区分用户模式和内核模式驱动程序体系结构模型。</li>
<li>了解加载的驱动程序以及 Windows 如何整理插 (PnP) 设备的设备树和设备节点中。 您还应了解如何 PnP 管理器生成设备堆栈和在设备堆栈中放置您的驱动程序和其设备对象的位置。</li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>步骤 6</strong>-准备您的开发和调试环境。</p>
<ul>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=617580" data-raw-source="[Install the latest Windows Driver Kit (WDK)](https://go.microsoft.com/fwlink/p/?linkid=617580)">安装最新的 Windows Driver Kit (WDK)</a>。</li>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=617580" data-raw-source="[Install Microsoft Visual Studio 2012](https://go.microsoft.com/fwlink/p/?linkid=617580)">安装 Microsoft Visual Studio 2012</a>。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/getting-set-up-for-debugging" data-raw-source="[Get Set Up for Debugging](https://docs.microsoft.com/windows-hardware/drivers/debugger/getting-set-up-for-debugging)">获取或设置最多用于调试</a>。</li>
<li>请确保你拥有<a href="headers-and-libraries-for-a-usb-client-driver.md" data-raw-source="[Headers and libraries required by a USB client driver](headers-and-libraries-for-a-usb-client-driver.md)">标头和库所需的 USB 客户端驱动程序</a>。</li>
</ul></td>
<td><ul>
<li>如果你正在编写一个内核模式驱动程序，应配置在主机和目标计算机上通过以太网网络、 1394年电缆、 USB 2.0 或 3.0 调试缆线或调制解调器电缆进行调试。</li>
<li>如果你正在编写的用户模式驱动程序，您可以使用 Microsoft Visual Studio 环境中可用的用户模式下调试。 您应该知道<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/debugging-a-user-mode-process-using-visual-studio" data-raw-source="[how to attach to a process or launch a process under the debugger](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugging-a-user-mode-process-using-visual-studio)">如何附加到进程或启动的进程在调试器下</a>。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>步骤 7</strong>— 编写您的第一个驱动程序。</p>
<ul>
<li><a href="tutorial--write-your-first-usb-client-driver--kmdf-.md" data-raw-source="[How to write your first USB client driver (KMDF)](tutorial--write-your-first-usb-client-driver--kmdf-.md)">如何编写第一个 USB 客户端驱动程序 (KMDF)</a></li>
<li><a href="implement-driver-entry-for-a-usb-driver--umdf-.md" data-raw-source="[How to write your first USB client driver (UMDF)](implement-driver-entry-for-a-usb-driver--umdf-.md)">如何编写第一个 USB 客户端驱动程序 (UMDF)</a></li>
</ul></td>
<td>编写、 构建和使用 Visual Studio 2012 中包含的 USB 模板安装第一个 USB 客户端驱动程序。 您应能够描述框架驱动程序、 设备和队列对象，并了解该框架与您的驱动程序的通信方式。</td>
</tr>
<tr class="even">
<td><strong>步骤 8</strong>-扩展您的驱动程序通过发送 USB 控制传输请求。</td>
<td>将标准控制请求和供应商命令发送到你的设备。 有关详细信息，请参阅<a href="usb-control-transfer.md" data-raw-source="[How to send a USB control transfer](usb-control-transfer.md)">如何发送 USB 控制传输</a>。</td>
</tr>
<tr class="odd">
<td><p><strong>步骤 9</strong>-扩展您的驱动程序可以使用 WDF USB I/O 目标对象执行 USB 数据传输。 <a href="usb-device-i-o.md" data-raw-source="[USB data transfers](usb-device-i-o.md)">USB 数据传输</a>。</p></td>
<td><p>扩展您的驱动程序以执行常见任务。 本主题列出了"如何"中此文档集的主题，提供了有关这些任务的分步指导。</p>
<ul>
<li><a href="wdk-resources-for-usb-driver-development.md" data-raw-source="[Common tasks for USB client drivers](wdk-resources-for-usb-driver-development.md)">USB 客户端驱动程序的常见任务</a></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="community-resources-for-usb"></a>有关 USB 的社区资源


<a href="" id="microsoft-windows-usb-core-team-blog"></a>[Microsoft Windows USB 核心团队博客](https://go.microsoft.com/fwlink/p/?linkid=617581)  
查看 Microsoft USB 团队撰写的博文。 此博客重点介绍 Windows USB 驱动程序堆栈，该堆栈适用于 Windows 电脑中的各种 USB 主控制器和 USB 集线器。 适用于 USB 客户端驱动程序开发人员和 USB 硬件设计人员的资源，方便他们了解驱动程序堆栈实现、解决常见问题以及如何使用工具来收集跟踪和日志文件。

<a href="" id="osr-online-lists---ntdev"></a>[OSR Online 列表-ntdev](https://go.microsoft.com/fwlink/p/?linkid=617582)  
由 [OSR Online](https://go.microsoft.com/fwlink/p/?linkid=617590) 管理的讨论列表，适用于内核模式驱动程序开发人员。

<a href="" id="usb-technologies"></a>[USB 技术](https://go.microsoft.com/fwlink/p/?linkid=617583)  
各种基于常见问题的资源，这些问题由不熟悉 Windows 操作系统的 USB 设备和驱动程序开发的开发人员提出。

<a href="" id="windows-dev-center-for-hardware-development"></a>[Windows 开发人员中心硬件开发](https://go.microsoft.com/fwlink/p/?linkid=617584)  
[下载最新驱动程序的开发工具](https://go.microsoft.com/fwlink/p/?linkid=617585)，确保您的产品可靠且与通过 Windows 兼容[Windows 认证计划](https://go.microsoft.com/fwlink/p/?linkid=617591)，了解[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507).

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB) 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/)  
[如何启用 USB 选择性挂起和系统唤醒 USB 设备在 UMDF 驱动程序中](https://go.microsoft.com/fwlink/p/?linkid=617587)  
[USB 驱动程序开发指南](usb-driver-development-guide.md)  



