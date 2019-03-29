---
Description: 在 Windows 8.1 中引入的 Windows 运行时 Api 用于编写允许用户访问其外围的 USB 设备的 UWP 应用。
title: 与 USB 设备通信，从开始到完成（UWP 应用）
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dba4c150128653fc2a724408bc1b70c6fb531871
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464351"
---
# <a name="talking-to-usb-devices-start-to-finish-uwp-app"></a>与 USB 设备通信，从开始到完成（UWP 应用）


**摘要**

-   创建 UWP 应用的端到端演练与 USB 设备
-   **配套示例**:[自定义的 USB 设备访问示例](https://go.microsoft.com/fwlink/p/?linkid=309716)

**重要的 Api**

-   [**Windows.Devices.Usb**](https://msdn.microsoft.com/library/windows/apps/dn278466)
-   [**Windows.Devices.Enumeration**](https://msdn.microsoft.com/library/windows/apps/br225459)
-   [**Windows.Devices.Background**](https://msdn.microsoft.com/library/windows/apps/dn263409)

在 Windows 8.1 中引入的 Windows 运行时 Api 用于编写允许用户访问其外围的 USB 设备的 UWP 应用。 此类应用程序可以连接到基于用户指定的条件的设备、 获取有关设备的信息、 将数据发送到设备并与之相反从设备中，获取数据流和轮询中断数据的设备。

此处介绍，如何使用 c + +，UWP 应用C#，或 Visual Basic 应用程序可以实现这些任务，并将链接到演示中包括的类的用法的示例[ **Windows.Devices.Usb**](https://msdn.microsoft.com/library/windows/apps/dn278466)。 我们将通过应用程序清单中所需的设备功能以及如何在设备连接时启动应用。 并且，我们将介绍如何进行数据传输任务在后台运行甚至当挂起应用程序时要维护电池寿命。

按照本部分中的步骤，或直接跳到[自定义 USB 设备访问示例](https://go.microsoft.com/fwlink/p/?linkid=309716)。 随附示例实现所有此处的步骤，但若要保持我们不会向通过代码。 某些步骤会随之**在此示例中找到该**部分来帮助你快速找到的代码。 示例的源代码文件的结构是简单和平面，因此您可以轻松地找到代码，而无需向下钻取的源代码文件的多个层。 但您可能更倾向于进行分解和组织您自己的项目，以不同的方式。

## <a name="in-this-section"></a>本节内容


-   [**步骤 1**— 功能为你的设备驱动程序，安装由 Microsoft 提供 WinUSB 驱动程序。](#step1)
-   [**步骤 2**-Get 设备接口的 GUID、 硬件 ID 和有关你的设备的设备类信息。](#step2)
-   [**步骤 3**-确定是否设置了设备类、 子类和 Windows 运行时 USB API 允许的协议。](#step3)
-   [**步骤 4**— 创建基本的 Microsoft Visual Studio 2013 项目，您可以充分利用本教程中。](#step4)
-   [**步骤 5**— 添加 USB 设备功能到应用程序清单。](#step5)
-   [**步骤 6**— 扩展应用程序以打开通信设备。](#step6)
-   [**步骤 7**— 研究您的 USB 设备布局。（推荐）](#step7)
-   [**步骤 8**— 扩展应用程序以获取并显示在 UI 中的 USB 描述符。](#step8)
-   [**步骤 9**— 扩展应用程序以发送供应商定义的 USB 控制传输。](#step9)
-   [**步骤 10**— 扩展应用程序以读取或写入大容量数据。](#step10)
-   [**步骤 11**— 扩展应用程序以获取硬件中断数据。](#step11)
-   [**步骤 12**— 扩展应用程序以选择不是当前处于活动状态的接口设置。](#step12)
-   [**步骤 13**— 关闭设备。](#step13)
-   [**步骤 14**— 创建设备元数据包用于应用程序。](#step14)
-   [**步骤 15**— 扩展应用程序以实现自动播放激活，以便在设备连接到系统时启动应用程序。](#step15)
-   [**步骤 16**— 扩展应用程序以实现可执行耗时较长的 USB 传输到设备，如固件更新，而无需获取挂起的应用的后台任务。](#step16)
-   [**步骤 17**— 运行 Windows 应用认证工具包。](#step17)

## <a name="walkthroughwriting-uwp-app-for-usb-devices"></a>演练-适用于 USB 设备的写入 UWP 应用


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>步骤</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="" id="step1"></a>
<p><strong>步骤 1</strong>— 功能为你的设备驱动程序，安装由 Microsoft 提供 WinUSB 驱动程序。</p></td>
<td><p><strong>快速入门：</strong><a href="winusb-installation.md" data-raw-source="[WinUSB (Winusb.sys) Installation](winusb-installation.md)">WinUSB (Winusb.sys) 安装</a></p>
<p>您可通过以下方式安装 Winusb.sys:</p>
<ul>
<li>当连接你的设备时，可能会注意到，Windows Winusb.sys 会自动加载，因为设备为<a href="automatic-installation-of-winusb.md" data-raw-source="[WinUSB Device](automatic-installation-of-winusb.md)">WinUSB 设备</a>。</li>
<li>通过指定的系统提供的设备类设备管理器中安装驱动程序。</li>
<li>使用自定义 INF 安装驱动程序。 可通过以下两种方式获取 INF:
<ul>
<li>从硬件供应商获取 INF。</li>
<li>编写引用由 Microsoft 提供 Winusb.inf 文件自定义 INF。 有关详细信息，请参阅<a href="winusb-installation.md" data-raw-source="[WinUSB (Winusb.sys) Installation](winusb-installation.md)">WinUSB (Winusb.sys) 安装</a>。</li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td><a href="" id="step2"></a>
<p><strong>步骤 2</strong>-Get 设备接口的 GUID、 硬件 ID 和有关你的设备的设备类信息。</p></td>
<td><p>您可以从设备制造商获取该信息。</p>
<ul>
<li><p><strong>供应商和产品标识符</strong></p>
<p>在设备管理器中，查看设备属性。 上<strong>详细信息</strong>选项卡上，查看<strong>硬件 Id</strong>属性值。 该值是这些两个标识符的组合。 例如，对于 SuperMUTT 设备<strong>硬件 Id</strong>是"USB\VID_045E&amp;PID_F001"; 供应商 ID 为"0x045E"，产品 ID 为"0xF001"。</p></li>
<li><strong>设备类、 子类和协议代码</strong></li>
<li><strong>设备接口的 GUID</strong></li>
</ul>
或者，可以查看注册表的信息。 有关详细信息，请参阅<a href="usb-device-specific-registry-settings.md" data-raw-source="[USB Device Registry Entries](usb-device-specific-registry-settings.md)">USB 设备注册表条目</a>。</td>
</tr>
<tr class="odd">
<td><a href="" id="step3"></a>
<p><strong>步骤 3</strong>-确定是否设置了设备类、 子类和 Windows 运行时 USB API 允许的协议。</p></td>
<td><p>您可以编写一个 UWP 应用，如果设备类、 子类和协议的设备的代码是以下之一：</p>
<ul>
<li><code>name:cdcControl,           classId:02 * *</code></li>
<li><code>name:physical, classId:05 * *</code></li>
<li><code>name:personalHealthcare,   classId:0f 00 00</code></li>
<li><code>name:activeSync,           classId:ef 01 01</code></li>
<li><code>name:palmSync,             classId:ef 01 02</code></li>
<li><code>name:deviceFirmwareUpdate, classId:fe 01 01</code></li>
<li><code>name:irda,                 classId:fe 02 00     </code></li>
<li><code>name:measurement,          classId:fe 03 *</code></li>
<li><code>name:vendorSpecific,       classId:ff * *</code></li>
</ul></td>
</tr>
<tr class="even">
<td><a href="" id="step4"></a>
<p><strong>步骤 4</strong>— 创建基本的 Visual Studio 2013 项目，您可以充分利用本教程中。</p></td>
<td>有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=617681" data-raw-source="[Getting started with UWP apps](https://go.microsoft.com/fwlink/p/?linkid=617681)">UWP 应用入门</a>。</td>
</tr>
<tr class="odd">
<td><a href="" id="step5"></a>
<p><strong>步骤 5</strong>— 添加 USB 设备功能到应用程序清单。</p></td>
<td><p><strong>快速入门：</strong><a href="updating-the-app-manifest-with-usb-device-capabilities.md" data-raw-source="[How to add USB device capabilities to the app manifest](updating-the-app-manifest-with-usb-device-capabilities.md)">如何将 USB 设备功能添加到应用程序清单</a></p>
<p>在文本编辑器中打开 Package.appxmanifest 文件并添加<a href="https://msdn.microsoft.com/library/windows/apps/br211430" data-raw-source="[&lt;strong&gt;DeviceCapability&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br211430)"> <strong>DeviceCapability</strong> </a>具有元素<strong>名称</strong>属性设置为"usb"中，在此示例中所示。</p>
<div class="alert">
<strong>请注意</strong>  不能修改 Visual Studio 2013 中的 USB 设备功能。 您必须右键单击 Package.appxmanifest 文件中的<strong>解决方案资源管理器</strong>，然后选择<strong>打开方式...</strong>，然后<strong>XML （文本） 编辑器</strong>。 在纯 XML 中打开该文件。
</div>
<div>
 
</div>
<pre class="syntax" space="preserve"><code>&lt;Capabilities&gt;
      &lt;!--When the device's classId is FF * *, there is a predefined name for the class. 
          You can use the name instead of the class id. 
          There are also other predefined names that correspond to a classId.--&gt;
      &lt;m2:DeviceCapability Name="usb"&gt;
          &lt;!--SuperMutt Device--&gt;
          &lt;m2:Device Id="vidpid:045E 0611"&gt;
              &lt;!--&lt;wb:Function Type="classId:ff * *"/&gt;--&gt;
              &lt;m2:Function Type="name:vendorSpecific"/&gt;
          &lt;/m2:Device&gt;
      &lt;/m2:DeviceCapability&gt;
  &lt;/Capabilities&gt;</code></pre>
<div class="code">

</div>
<p><strong>在此示例中找到它：</strong>在 Package.appxmanifest 文件中添加的 USB 设备功能。</p></td>
</tr>
<tr class="even">
<td><a href="" id="step6"></a>
<p><strong>步骤 6</strong>— 扩展应用程序以打开通信设备。</p></td>
<td><p><strong>快速入门：</strong><a href="how-to-connect-to-a-usb-device--uwp-app-.md" data-raw-source="[How to connect to a USB device (UWP app)](how-to-connect-to-a-usb-device--uwp-app-.md)">如何连接到 USB 设备 （UWP 应用）</a></p>
<ol>
<li>通过构建一个高级查询语法 (AQS) 字符串，包含搜索条件以查找设备枚举的设备集合中查找设备。</li>
<li>在两种方式之一打开设备：
<ul>
<li><p>传递到 AQS <a href="https://msdn.microsoft.com/library/windows/apps/br225432" data-raw-source="[&lt;strong&gt;FindAllAsync&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225432)"> <strong>FindAllAsync</strong> </a> ，并获取<a href="https://msdn.microsoft.com/library/windows/apps/br225393" data-raw-source="[&lt;strong&gt;DeviceInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225393)"> <strong>DeviceInformation</strong> </a>设备对象。</p>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/apps/xaml/hh872189" data-raw-source="[Quickstart: enumerating commonly used devices](https://msdn.microsoft.com/library/windows/apps/xaml/hh872189)">快速入门： 枚举通常使用设备</a>。</p></li>
<li>通过使用<a href="https://msdn.microsoft.com/library/windows/apps/br225446" data-raw-source="[&lt;strong&gt;DeviceWatcher&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225446)"> <strong>DeviceWatcher</strong> </a>对象无法检测何时添加或从系统中删除设备。
<ol>
<li>传递到 AQS <a href="https://msdn.microsoft.com/library/windows/apps/br225427" data-raw-source="[&lt;strong&gt;CreateWatcher&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225427)"> <strong>CreateWatcher</strong> </a> ，并获取<a href="https://msdn.microsoft.com/library/windows/apps/br225446" data-raw-source="[&lt;strong&gt;DeviceWatcher&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225446)"> <strong>DeviceWatcher</strong> </a>对象。</li>
<li>在注册事件处理程序<a href="https://msdn.microsoft.com/library/windows/apps/br225446" data-raw-source="[&lt;strong&gt;DeviceWatcher&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225446)"> <strong>DeviceWatcher</strong> </a>对象。</li>
<li>获取<a href="https://msdn.microsoft.com/library/windows/apps/br225393" data-raw-source="[&lt;strong&gt;DeviceInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225393)"> <strong>DeviceInformation</strong> </a>对象中的设备应用<a href="https://msdn.microsoft.com/library/windows/apps/br225450" data-raw-source="[&lt;strong&gt;Added&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225450)"> <strong>Added</strong> </a>事件处理程序。</li>
<li>启动和停止<a href="https://msdn.microsoft.com/library/windows/apps/br225446" data-raw-source="[&lt;strong&gt;DeviceWatcher&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225446)"> <strong>DeviceWatcher</strong> </a>对象。</li>
</ol>
有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/apps/xaml/hh967756" data-raw-source="[How to get notifications if devices are added, removed, or changed](https://msdn.microsoft.com/library/windows/apps/xaml/hh967756)">如何获取通知，如果设备被添加、 移除或更改</a>。</li>
</ul></li>
<li>获取从设备实例<a href="https://msdn.microsoft.com/library/windows/apps/br225437" data-raw-source="[&lt;strong&gt;DeviceInformation.Id&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225437)"> <strong>DeviceInformation.Id</strong> </a>属性。</li>
<li>调用<a href="https://msdn.microsoft.com/library/windows/apps/dn264010" data-raw-source="[&lt;strong&gt;FromIdAsync&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264010)"> <strong>FromIdAsync</strong> </a>通过设备实例字符串和 get <a href="https://msdn.microsoft.com/library/windows/apps/dn263883" data-raw-source="[&lt;strong&gt;UsbDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn263883)"> <strong>UsbDevice</strong> </a>对象。</li>
</ol>
<p><strong>在此示例中找到它：</strong>请参阅名为 Scenario1_DeviceConnect 的文件。</p></td>
</tr>
<tr class="odd">
<td><a href="" id="step7"></a>
<p><strong>步骤 7</strong>（推荐） — 研究您<a href="usb-device-layout.md" data-raw-source="[USB device layout](usb-device-layout.md)">USB 设备布局</a>。</p></td>
<td><p>查看有关配置设备和执行数据传输基本 USB 概念：<a href="usb-concepts-for-all-developers.md" data-raw-source="[Concepts for all USB developers](usb-concepts-for-all-developers.md)">为所有 USB 开发人员概念</a>。</p>
<p>查看设备配置描述符、 每个受支持的替代设置的接口描述符和其终结点描述符。 通过使用<a href="https://go.microsoft.com/fwlink/p/?linkid=617721" data-raw-source="[USBView](https://go.microsoft.com/fwlink/p/?linkid=617721)">USBView</a>，可以浏览所有 USB 控制器和 USB 设备连接到它们，并还检查设备配置。</p></td>
</tr>
<tr class="even">
<td><a href="" id="step8"></a>
<p><strong>步骤 8</strong>— 扩展应用程序以获取并显示在 UI 中的 USB 描述符。</p></td>
<td><p><strong>快速入门：</strong><a href="how-to-get-usb-descriptors--uwp-app-.md" data-raw-source="[How to get USB descriptors (UWP app)](how-to-get-usb-descriptors--uwp-app-.md)">如何获取 USB 描述符 （UWP 应用）</a></p>
<p></p>
<ul>
<li>通过获取获取的设备描述符<a href="https://msdn.microsoft.com/library/windows/apps/dn264002" data-raw-source="[&lt;strong&gt;UsbDevice.DeviceDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264002)"> <strong>UsbDevice.DeviceDescriptor</strong> </a>值。</li>
<li>获取通过获取 configuration 描述符<a href="https://msdn.microsoft.com/library/windows/apps/dn263799" data-raw-source="[&lt;strong&gt;UsbConfiguration.ConfigurationDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn263799)"> <strong>UsbConfiguration.ConfigurationDescriptor</strong> </a>值。
<ul>
<li>获取通过获取设置的完整配置描述符<a href="https://msdn.microsoft.com/library/windows/apps/dn263802" data-raw-source="[&lt;strong&gt;UsbConfiguration.Descriptors&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn263802)"> <strong>UsbConfiguration.Descriptors</strong> </a>属性。</li>
</ul></li>
<li>通过获取获取配置中的接口的数组<a href="https://msdn.microsoft.com/library/windows/apps/dn263808" data-raw-source="[&lt;strong&gt;UsbConfiguration.UsbInterfaces&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn263808)"> <strong>UsbConfiguration.UsbInterfaces</strong> </a>属性。</li>
<li>通过获取获取替代设置的数组<a href="https://msdn.microsoft.com/library/windows/apps/dn264291" data-raw-source="[&lt;strong&gt;UsbInterface.InterfaceSettings&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264291)"> <strong>UsbInterface.InterfaceSettings</strong></a>。</li>
<li><p>在活动备用设置枚举管道并获取关联的终结点。</p>
<p>由这些对象表示终结点描述符：</p>
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/apps/dn297543" data-raw-source="[&lt;strong&gt;UsbBulkInEndpointDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn297543)"><strong>UsbBulkInEndpointDescriptor</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/apps/dn297619" data-raw-source="[&lt;strong&gt;UsbBulkOutEndpointDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn297619)"><strong>UsbBulkOutEndpointDescriptor</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/apps/dn264294" data-raw-source="[&lt;strong&gt;UsbInterruptInEndpointDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264294)"><strong>UsbInterruptInEndpointDescriptor</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/apps/dn278420" data-raw-source="[&lt;strong&gt;UsbInterruptOutEndpointDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278420)"><strong>UsbInterruptOutEndpointDescriptor</strong></a></li>
</ul></li>
</ul>
<p><strong>在此示例中找到它：</strong>请参阅名为 Scenario5_UsbDescriptors 的文件。</p></td>
</tr>
<tr class="odd">
<td><a href="" id="step9"></a>
<p><strong>步骤 9</strong>— 扩展应用程序以发送供应商定义的 USB 控制传输。</p></td>
<td><p><strong>快速入门：</strong><a href="how-to-send-a-usb-control-transfer--uwp-app-.md" data-raw-source="[How to send a USB control transfer request (UWP app)](how-to-send-a-usb-control-transfer--uwp-app-.md)">如何发送 USB 控制传输请求 （UWP 应用）</a></p>
<p></p>
<ol>
<li>从设备的硬件规格获取供应商命令。</li>
<li>创建<a href="https://msdn.microsoft.com/library/windows/apps/dn278431" data-raw-source="[&lt;strong&gt;UsbSetupPacket&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278431)"> <strong>UsbSetupPacket</strong> </a>对象，并通过设置各种属性填充安装数据包。</li>
<li>启动异步操作以发送控制传输通过这些方法，具体取决于传输的方向：
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/apps/dn264027" data-raw-source="[&lt;strong&gt;SendControlInTransferAsync&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264027)"><strong>SendControlInTransferAsync</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/apps/dn264044" data-raw-source="[&lt;strong&gt;SendControlOutTransferAsync&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264044)"><strong>SendControlOutTransferAsync</strong></a></li>
</ul></li>
</ol>
<p><strong>在此示例中找到它：</strong>请参阅名为 Scenario2_ControlTransfer 的文件。</p></td>
</tr>
<tr class="even">
<td><a href="" id="step10"></a>
<p><strong>步骤 10</strong>— 扩展应用程序以读取或写入大容量数据。</p></td>
<td><p><strong>快速入门：</strong><a href="how-to-send-a-usb-bulk-transfer--uwp-app-.md" data-raw-source="[How to send a USB bulk transfer request (UWP app)](how-to-send-a-usb-bulk-transfer--uwp-app-.md)">如何将发送的 USB 大容量传输请求 （UWP 应用）</a></p>
<p></p>
<ol>
<li>获取大容量的管道对象 (<a href="https://msdn.microsoft.com/library/windows/apps/dn297647" data-raw-source="[&lt;strong&gt;UsbBulkOutPipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn297647)"><strong>UsbBulkOutPipe</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/apps/dn297573" data-raw-source="[&lt;strong&gt;UsbBulkInPipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn297573)"> <strong>UsbBulkInPipe</strong></a>)。</li>
<li>配置大容量管道设置策略参数。</li>
<li>使用设置的数据流<a href="https://msdn.microsoft.com/library/windows/apps/br208119" data-raw-source="[&lt;strong&gt;DataReader&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br208119)"> <strong>DataReader</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/apps/br208154" data-raw-source="[&lt;strong&gt;DataWriter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br208154)"> <strong>DataWriter</strong> </a>对象。</li>
<li>启动异步传输操作通过调用<a href="https://msdn.microsoft.com/library/windows/apps/br208135" data-raw-source="[&lt;strong&gt;DataReader.LoadAsync&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br208135)"> <strong>DataReader.LoadAsync</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/apps/br208171" data-raw-source="[&lt;strong&gt;DataWriter.StoreAsync&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br208171)"> <strong>DataWriter.StoreAsync</strong></a>。</li>
<li>获取在传输操作的结果。</li>
</ol>
<p><strong>在此示例中找到它：</strong>请参阅名为 Scenario4_BulkPipes 的文件。</p></td>
</tr>
<tr class="odd">
<td><a href="" id="step11"></a>
<p><strong>步骤 11</strong>— 扩展应用程序以获取硬件中断数据。</p></td>
<td><p><strong>快速入门：</strong><a href="how-to-send-a-usb-interrupt-transfer--uwp-app-.md" data-raw-source="[How to send a USB interrupt transfer request (UWP app)](how-to-send-a-usb-interrupt-transfer--uwp-app-.md)">如何发送 USB 中断传输请求 （UWP 应用）</a></p>
<p></p>
<ol>
<li>获取中断管道对象 (<a href="https://msdn.microsoft.com/library/windows/apps/dn278416" data-raw-source="[&lt;strong&gt;UsbInterruptInPipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278416)"><strong>UsbInterruptInPipe</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/apps/dn278425" data-raw-source="[&lt;strong&gt;UsbInterruptOutPipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278425)"> <strong>UsbInterruptOutPipe</strong></a>)。</li>
<li>实现的中断处理程序<a href="https://msdn.microsoft.com/library/windows/apps/dn278418" data-raw-source="[&lt;strong&gt;DataReceived&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278418)"> <strong>DataReceived</strong> </a>事件。</li>
<li>注册要开始接收数据的事件处理程序。</li>
<li>注销要停止接收数据的事件处理程序。</li>
</ol>
<p><strong>在此示例中找到它：</strong>请参阅名为 Scenario3_InterruptPipes 的文件。</p></td>
</tr>
<tr class="even">
<td><a href="" id="step12"></a>
<p><strong>步骤 12</strong>— 扩展应用程序以选择不是当前处于活动状态的接口设置。</p></td>
<td><p><strong>快速入门：</strong><a href="how-to-select-a-usb-interface-setting--uwp-app-.md" data-raw-source="[How to select a USB interface setting (UWP app)](how-to-select-a-usb-interface-setting--uwp-app-.md)">如何选择 USB 接口设置 （UWP 应用）</a></p>
<p>当设备打开进行通信时，选择默认接口和其第一个设置。 如果你想要更改该设置，请执行以下步骤：</p>
<ol>
<li>使用获取 USB 接口的活动设置<a href="https://msdn.microsoft.com/library/windows/apps/dn264285" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting.Selected&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264285)"> <strong>UsbInterfaceSetting.Selected</strong> </a>值。</li>
<li>通过调用开始异步操作来设置 USB 接口设置<a href="https://msdn.microsoft.com/library/windows/apps/dn264286" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting.SelectSettingAsync&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264286)"> <strong>UsbInterfaceSetting.SelectSettingAsync</strong></a>。</li>
</ol></td>
</tr>
<tr class="odd">
<td><a href="" id="step13"></a>
<p><strong>步骤 13</strong>— 关闭设备。</p></td>
<td><p><strong>快速入门：</strong><a href="how-to-connect-to-a-usb-device--uwp-app-.md" data-raw-source="[How to connect to a USB device (UWP app)](how-to-connect-to-a-usb-device--uwp-app-.md)">如何连接到 USB 设备 （UWP 应用）</a></p>
<p>在使用完 UsbDevice 对象后，关闭设备。</p>
<p>C + + 应用程序必须通过使用发布的引用<strong>删除</strong>关键字。 C#/VB 应用必须调用<a href="https://msdn.microsoft.com/library/windows/apps/dn264007" data-raw-source="[&lt;strong&gt;UsbDevice.Dispose&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264007)"> <strong>UsbDevice.Dispose</strong> </a>方法。 JavaScript 应用程序必须调用<a href="https://msdn.microsoft.com/library/windows/apps/dn263990" data-raw-source="[&lt;strong&gt;UsbDevice.Close&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn263990)"> <strong>UsbDevice.Close</strong></a>。</p>
<p><strong>在此示例中找到它：</strong>请参阅名为 Scenario1_DeviceConnect 的文件。</p></td>
</tr>
<tr class="even">
<td><a href="" id="step14"></a>
<p><strong>步骤 14</strong>— 创建设备元数据包用于应用程序。</p></td>
<td><strong>工具：</strong><a href="https://msdn.microsoft.com/library/windows/hardware/hh454213" data-raw-source="[Device Metadata Authoring Wizard](https://msdn.microsoft.com/library/windows/hardware/hh454213)">设备元数据创建向导</a>
<ul>
<li>如果您有 Windows Driver Kit (WDK) 安装，打开<strong>驱动程序</strong> &gt; <strong>设备元数据</strong> &gt; <strong>创作</strong>。</li>
<li>如果你有独立安装 SDK，该工具位于 <em>&lt;install_path&gt;</em>\bin\x86\DeviceMetadataWizardexe。</li>
</ul>
<p>将您的应用程序与设备关联按照向导中的步骤。 输入有关你的设备的信息：</p>
<p></p>
<ul>
<li>上<strong>设备信息</strong>页上，输入<strong>模型名称</strong>，<strong>制造商</strong>，以及<strong>说明</strong>。</li>
<li>上<strong>硬件信息</strong>页上，输入你的设备的硬件 ID。</li>
</ul>
<p><strong>若要将应用程序声明为用于你的设备的特权应用程序，请按照以下说明：</strong></p>
<ol>
<li><p>上<strong>应用信息</strong>页上，在<strong>特权应用程序</strong>组中，输入<strong>包名称</strong>，<strong>发布者名称</strong>，和<strong>UWP 应用程序 ID</strong>。</p>
<p><img src="images/privileged-app.png" alt="device metatdata for privileged apps" /></p>
<div class="alert">
<strong>请注意</strong>  不会检查<strong>Access 自定义驱动程序</strong>选项。
</div>
<div>
 
</div></li>
<li>打开<strong>完成</strong>选项卡。选择<strong>将包复制到您的系统的本地元数据存储</strong>复选框。</li>
<li>连接设备，在控件面板中，打开<strong>查看设备和打印机</strong>并验证设备的图标是否正确。</li>
</ol>
<p><strong>在此示例中找到它：</strong>请参阅 DeviceMetadata 文件夹。</p></td>
</tr>
<tr class="odd">
<td><a href="" id="step15"></a>
<p><strong>步骤 15</strong>— 扩展应用程序以实现自动播放激活，以便在设备连接到系统时启动应用程序。</p></td>
<td><p><strong>快速入门：</strong><a href="https://msdn.microsoft.com/library/windows/apps/xaml/jj161017" data-raw-source="[Register an app for an AutoPlay device](https://msdn.microsoft.com/library/windows/apps/xaml/jj161017)">注册自动播放设备的应用</a></p>
<p>您可以添加自动播放功能，以便在设备连接到系统时启动该应用程序。 适用于所有 UWP 应用 （特权或其他方式），可以启用自动播放。</p>
<p></p>
<ol>
<li>在你设备元数据包，必须指定设备应如何响应的自动播放通知。 上<strong>Windows 信息</strong>选项卡上，选择<strong>UWP 设备应用</strong>选项并输入应用信息，如下所示：</li>
<li><p>在应用程序清单中，添加<strong>自动播放设备</strong>声明和启动信息如下所示：</p>
<p><img src="images/autoplay.png" alt="AutoPlay" /></p></li>
<li>在 App 类 OnActivated 方法中，选中是否设备激活应用程序。 如果是，则该方法接收 DeviceEventArgs 参数值，该值包含<a href="https://msdn.microsoft.com/library/windows/apps/br225437" data-raw-source="[&lt;strong&gt;DeviceInformation.Id&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225437)"> <strong>DeviceInformation.Id</strong> </a>属性值。 这是相同的值中所述<a href="#step6" data-raw-source="[&lt;strong&gt;Step 6&lt;/strong&gt;—Extend the app to open the device for communication](#step6)"><strong>第 6 步</strong>— 扩展应用程序以打开通信设备</a>。</li>
</ol>
<p><strong>在此示例中找到它：</strong>请参阅名为自动播放的文件。 JavaScript，请参阅 default.js。</p></td>
</tr>
<tr class="even">
<td><a href="" id="step16"></a>
<p><strong>步骤 16</strong>— 扩展应用程序以实现可执行长度传输到设备，如固件更新，而无需应用程序获取挂起的后台任务。</p></td>
<td><p>若要实现后台任务，您需要两个类。</p>
<p>后台任务类实现<a href="https://msdn.microsoft.com/library/windows/apps/br224794" data-raw-source="[&lt;strong&gt;IBackgroundTask&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br224794)"> <strong>IBackgroundTask</strong> </a>接口并包含到任一同步创建或更新外围设备的实际代码。 触发后台任务时，从你的应用的应用程序清单中提供的入口点执行后台任务类。</p>
<div class="alert">
<strong>请注意</strong>提供 Windows 8.1 的设备后台任务基础结构。 详细了解 Windows 后台任务，请参阅<a href="https://msdn.microsoft.com/library/windows/apps/xaml/hh977056" data-raw-source="[Supporting your app with background tasks](https://msdn.microsoft.com/library/windows/apps/xaml/hh977056)">支持使用后台任务对应用程序</a>。
</div>
<div>
 
</div>
<p><strong>后台任务类</strong></p>
<ol>
<li>实现<a href="https://msdn.microsoft.com/library/windows/apps/br224794" data-raw-source="[&lt;strong&gt;IBackgroundTask&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br224794)"> <strong>IBackgroundTask</strong> </a> Windows 后台任务基础结构所需的接口。</li>
<li>获取传递给中的类的 DeviceUseDetails 实例<strong>运行</strong>报告进度的此实例方法，并使用备份到 Microsoft Store 应用并注册取消事件。</li>
<li><strong>运行</strong>方法还会调用私有实现后台设备同步代码的 OpenDevice 和 WriteToDeviceAsync 方法。</li>
</ol>
<p>UWP 应用注册，并触发 DeviceUseTrigger 后台任务。 应用程序进行注册，触发器，并处理后台任务的进度。</p>
<div class="alert">
<strong>请注意</strong>  示例代码如下所示，可以应用于 DeviceServicingTrigger 后台任务通过使用相应的对象。 两个触发器对象和其相应的 Api 的唯一区别是所做的 Windows 策略检查。
</div>
<div>
 
</div>
<ol>
<li>创建 DeviceUseTrigger 和 BackgroundTaskRegistration 对象。</li>
<li>检查是否任何后台任务之前已注册此示例应用程序，并取消它们通过取消注册的方法调用的任务。</li>
<li>向设备注册将同步的后台任务。 SetupBackgroundTask 方法是从下一步中 SyncWithDeviceAsync 方法调用。
<ol>
<li>初始化 DeviceUseTrigger 并将其保存以供将来使用。</li>
<li>创建 BackgroundTaskBuilder 对象并使用其名称、 TaskEntryPoint 和 SetTrigger 属性和方法来注册应用程序的 DeviceUseTrigger 对象和后台任务的名称。 BackgroundTaskBuilder 对象 TaskEntryPoint 属性设置为触发后台任务时都会运行的后台任务类的全名。</li>
<li>注册的完成和从后台任务的进度事件，以便 Microsoft Store 应用程序可以向用户提供完成和正在进行更新。</li>
</ol></li>
<li>专用 SyncWithDeviceAsync 方法注册的后台任务，将设备与同步启动后台同步。
<ol>
<li>从上一步调用 SetupBackgroundTask 方法并向设备注册将同步的后台任务。</li>
<li>调用私有 StartSyncBackgroundTaskAsync 方法启动的后台任务。</li>
<li>关闭到设备以确保后台任务可以在启动时打开设备的应用程序的句柄。
<div class="alert">
<strong>请注意</strong>  后台任务将需要打开设备以执行更新，因此 Microsoft Store 应用程序必须调用 RequestAsync 之前关闭其与设备的连接
</div>
<div>
 
</div></li>
<li>调用 DeviceUseTrigger 对象的 RequestAsync 方法启动触发器的后台任务并返回从 RequestAsync DeviceTriggerResults 对象用于确定是否已成功启动后台任务。
<div class="alert">
<strong>请注意</strong>  Windows 进行检查以确保所有必需的任务启动策略检查已完成。 如果所有策略都检查都已完成更新操作现在作为后台任务之外的 Microsoft Store 应用，可通过应用程序安全地挂起操作正在进行时运行。 Windows 还将强制执行任何运行时要求，并取消后台任务，如果不再满足这些要求。
</div>
<div>
 
</div></li>
<li>使用从 StartSyncBackgroundTaskAsync 返回 DeviceTriggerResults 对象来确定是否已成功启动后台任务。 Switch 语句用于检查 DeviceTriggerResults 的结果。</li>
</ol></li>
<li>实现将从后台任务的进度更新应用程序 UI 的专用 OnSyncWithDeviceProgress 事件处理程序。</li>
<li>实现专用的 OnSyncWithDeviceCompleted 事件处理程序以处理从后台任务转换为前台应用程序时的后台任务已完成。
<ol>
<li>使用 BackgroundTaskCompletedEventArgs 对象的 CheckResults 方法来确定是否的后台任务引发任何异常。</li>
<li>现在，后台任务已完成并更新 UI 以通知用户，应用程序重新打开该设备进行使用前台应用程序的情况。</li>
</ol></li>
<li>实现专用按钮单击事件处理程序从用户界面来启动和取消后台任务。
<ol>
<li>专用 Sync_Click 事件处理程序调用 SyncWithDeviceAsync 方法上一步骤中所述。</li>
<li>专用 CancelSync_Click 事件处理程序调用私有的 CancelSyncWithDevice 方法，以取消后台任务。</li>
</ol></li>
<li>私有 CancelSyncWithDevice 方法中取消注册和取消任何活动设备同步，以便该设备，也可以重新使用 BackgroundTaskRegistration 对象上的取消注册方法。</li>
</ol>
<p><strong>在此示例中找到它：</strong>请参阅名为 Scenario7_Sync 文件的文件。 背景类 IoSyncBackgroundTask 中实现。</p></td>
</tr>
<tr class="odd">
<td><a href="" id="step17"></a>
<p><strong>步骤 17</strong>— 运行 Windows 应用认证工具包。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/apps/hh694081" data-raw-source="[Using the Windows App Certification Kit](https://msdn.microsoft.com/library/windows/apps/hh694081)">使用 Windows 应用认证工具包</a></p>
<p>推荐。 运行 Windows 应用认证工具包，可帮助确保您的应用程序可满足 Microsoft Store 的要求，因此主要功能添加到您的应用程序时应执行此操作。</p></td>
</tr>
</tbody>
</table>

 

## <a name="want-to-know-more"></a>希望了解更多信息？


了解详细信息中的相关示例。

**相关的示例**

-   [USB CDC 控制示例](https://go.microsoft.com/fwlink/p/?linkid=309716)
-   [固件更新 USB 设备示例](https://go.microsoft.com/fwlink/p/?linkid=309716)

[UWP 应用 UI 中，启动以完成 (XAML)](https://msdn.microsoft.com/library/windows/apps/xaml/dn263191)

了解设计 UWP 应用程序 UI 的详细信息。

[使用的 UWP 应用的路线图C#和 Visual Basic](https://msdn.microsoft.com/library/windows/apps/br229583)并[使用 c + + 的 UWP 应用的路线图](https://msdn.microsoft.com/library/windows/apps/hh700360)

详细了解如何创建 UWP 应用使用 c + +， C#，或在常规中的 Visual Basic。

[异步编程（UWP 应用）](https://msdn.microsoft.com/library/windows/apps/hh464924)

了解有关如何使的应用保持响应时在起作用，可能需要一段较的长的时间。

 

 




