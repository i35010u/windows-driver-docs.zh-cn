---
description: 使用 Windows 8.1 中引入的 Windows 运行时 Api 编写允许用户访问其外围设备 USB 设备的 UWP 应用。
title: 与 USB 设备通信，从开始到完成（UWP 应用）
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64084c547c9c57b63473b7ded5d2360c0eac4a2e
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968680"
---
# <a name="talking-to-usb-devices-start-to-finish-uwp-app"></a>与 USB 设备通信，从开始到完成（UWP 应用）


**摘要**

-   用于创建与 USB 设备通信的 UWP 应用的端到端演练
-   **伴生示例**： [自定义 USB 设备访问示例](https://go.microsoft.com/fwlink/p/?linkid=309716)

**重要的 API**

-   [**Windows.Devices.Usb**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)
-   [**Windows.Devices.Enumeration**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration)
-   [**Windows. 后台**](https://docs.microsoft.com/uwp/api/Windows.Devices.Background)

使用 Windows 8.1 中引入的 Windows 运行时 Api 编写允许用户访问其外围设备 USB 设备的 UWP 应用。 此类应用程序可以基于用户指定的条件连接到设备、获取有关设备的信息、将数据发送到设备，并与从设备获取数据流相反，并轮询设备是否有中断数据。

本文介绍如何使用 c + +、c # 或 Visual Basic 应用程序的 UWP 应用程序如何实现这些任务，并链接到演示如何使用 [**Windows**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)中包含的类的示例。 我们将通过应用程序清单中所需的设备功能，以及在连接设备时如何启动应用。 同时，我们还将介绍如何在后台运行数据传输任务，即使应用程序已暂停以节省电池寿命。

按照本部分中的步骤或直接跳到 [自定义 USB 设备访问示例](https://go.microsoft.com/fwlink/p/?linkid=309716)。 随附示例实现了本文中的所有步骤，但若要继续操作，我们不会演练代码。 某些步骤 **在 "示例" 部分中找到了它** ，可帮助你快速找到代码。 该示例的源文件结构简单明了，因此您可以轻松地查找代码，而无需向下钻取多层源文件。 但您可能希望以不同的方式分解和组织您自己的项目。

## <a name="in-this-section"></a>本节内容


-   [**步骤 1**-将 Microsoft 提供的 WinUSB 驱动程序安装为设备的函数驱动程序。](#step1)
-   [**步骤 2**-获取设备接口 GUID、硬件 ID 和设备的设备类信息。](#step2)
-   [**步骤 3**-确定 WINDOWS 运行时 USB API 集是否允许的设备类、子类和协议。](#step3)
-   [**步骤 4**-创建可在本教程中扩展的基本 Microsoft Visual Studio 2013 项目。](#step4)
-   [**步骤 5**-将 USB 设备功能添加到应用程序清单。](#step5)
-   [**步骤 6**-扩展应用程序以打开设备进行通信。](#step6)
-   [**步骤 7**—研究 USB 设备布局。 (建议) ](#step7)
-   [**步骤 8**-扩展应用程序以在 UI 中获取和显示 USB 描述符。](#step8)
-   [**步骤 9**-扩展应用程序以发送供应商定义的 USB 控制传输。](#step9)
-   [**步骤 10**-扩展应用程序以读取或写入大容量数据。](#step10)
-   [**步骤 11**-扩展应用程序以获取硬件中断数据。](#step11)
-   [**步骤 12**-扩展应用以选择当前处于非活动状态的接口设置。](#step12)
-   [**步骤 13**-关闭设备。](#step13)
-   [**步骤 14**-为应用创建设备元数据包。](#step14)
-   [**步骤 15**-扩展应用程序以实现自动播放激活，以便在设备连接到系统时启动应用。](#step15)
-   [**步骤 16**：扩展应用程序以实现后台任务，该任务可对设备执行冗长的 USB 传输，如固件更新，而不会挂起应用。](#step16)
-   [**步骤 17**-运行 Windows 应用认证工具包。](#step17)

## <a name="walkthroughwriting-uwp-app-for-usb-devices"></a>演练-编写适用于 USB 设备的 UWP 应用


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>步骤</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="" id="step1"></a>
<p><strong>步骤 1</strong>-将 Microsoft 提供的 WinUSB 驱动程序安装为设备的函数驱动程序。</p></td>
<td><p><strong>快速入门：</strong> <a href="winusb-installation.md" data-raw-source="[WinUSB (Winusb.sys) Installation](winusb-installation.md)">WinUSB ( # A0) 安装</a></p>
<p>可以通过以下方式安装 Winusb.sys：</p>
<ul>
<li>连接设备时，可能会注意到，Windows 会自动加载 Winusb.sys 因为设备是 <a href="automatic-installation-of-winusb.md" data-raw-source="[WinUSB Device](automatic-installation-of-winusb.md)">WinUSB 设备</a>。</li>
<li>通过在设备管理器中指定系统提供的设备类来安装驱动程序。</li>
<li>使用自定义 INF 安装驱动程序。 可以通过以下两种方式之一获取 INF：
<ul>
<li>从硬件供应商处获取 INF。</li>
<li>编写引用 Microsoft 提供的 Winusb 文件的自定义 INF。 有关详细信息，请参阅 <a href="winusb-installation.md" data-raw-source="[WinUSB (Winusb.sys) Installation](winusb-installation.md)">WinUSB ( # A0) 安装</a>。</li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td><a href="" id="step2"></a>
<p><strong>步骤 2</strong>-获取设备接口 GUID、硬件 ID 和设备的设备类信息。</p></td>
<td><p>你可以从设备制造商处获取该信息。</p>
<ul>
<li><p><strong>供应商和产品标识符</strong></p>
<p>在设备管理器中，查看设备属性。 在 " <strong>详细信息</strong> " 选项卡上，查看 " <strong>硬件 Id</strong> " 属性值。 该值是这两个标识符的组合。 例如，对于 SuperMUTT 设备， <strong>硬件 Id</strong> 为 "USB \ VID_045E&PID_F001";供应商 ID 是 "0x045E"，product ID 为 "0xF001"。</p></li>
<li><strong>设备类、子类和协议代码</strong></li>
<li><strong>设备接口 GUID</strong></li>
</ul>
或者，可以查看注册表信息。 有关详细信息，请参阅 <a href="usb-device-specific-registry-settings.md" data-raw-source="[USB Device Registry Entries](usb-device-specific-registry-settings.md)">USB 设备注册表项</a>。</td>
</tr>
<tr class="odd">
<td><a href="" id="step3"></a>
<p><strong>步骤 3</strong>-确定 WINDOWS 运行时 USB API 集是否允许的设备类、子类和协议。</p></td>
<td><p>如果设备类、子类和设备的协议代码是下列其中一项，则可以编写 UWP 应用：</p>
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
<p><strong>步骤 4</strong>-创建可在本教程中扩展的基本 Visual Studio 2013 项目。</p></td>
<td>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=617681" data-raw-source="[Getting started with UWP apps](https://go.microsoft.com/fwlink/p/?linkid=617681)">UWP 应用</a>入门。</td>
</tr>
<tr class="odd">
<td><a href="" id="step5"></a>
<p><strong>步骤 5</strong>-将 USB 设备功能添加到应用程序清单。</p></td>
<td><p><strong>快速入门：</strong> <a href="updating-the-app-manifest-with-usb-device-capabilities.md" data-raw-source="[How to add USB device capabilities to the app manifest](updating-the-app-manifest-with-usb-device-capabilities.md)">如何将 USB 设备功能添加到应用程序清单</a></p>
<p>在文本编辑器中打开 appxmanifest.xml 文件，并添加<strong>Name</strong>属性设置为 "usb" 的<a href="https://docs.microsoft.com/uwp/schemas/appxpackage/appxmanifestschema/element-devicecapability" data-raw-source="[&lt;strong&gt;DeviceCapability&lt;/strong&gt;](https://docs.microsoft.com/uwp/schemas/appxpackage/appxmanifestschema/element-devicecapability)"><strong>DeviceCapability</strong></a>元素，如本示例中所示。</p>
<div class="alert">
<strong>注意</strong>   无法在 Visual Studio 2013 中修改 USB 设备功能。 必须右键单击 <strong>解决方案资源管理器</strong> 中的 appxmanifest.xml 文件，然后选择 " <strong>打开方式 ...</strong>"，然后选择 " <strong>XML (文本) 编辑器</strong>"。 文件以纯 XML 格式打开。
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
<p><strong>在示例中找到它：</strong> USB 设备功能将添加到 appxmanifest.xml 文件中。</p></td>
</tr>
<tr class="even">
<td><a href="" id="step6"></a>
<p><strong>步骤 6</strong>-扩展应用程序以打开设备进行通信。</p></td>
<td><p><strong>快速入门：</strong> <a href="how-to-connect-to-a-usb-device--uwp-app-.md" data-raw-source="[How to connect to a USB device (UWP app)](how-to-connect-to-a-usb-device--uwp-app-.md)">如何连接到 USB 设备 (UWP 应用) </a></p>
<ol>
<li>通过生成高级查询语法 (包含搜索条件（用于在枚举设备集合中查找设备）) 字符串来查找设备。</li>
<li>通过以下两种方式之一打开设备：
<ul>
<li><p>将 AQS 传递到 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation#Windows_Devices_Enumeration_DeviceInformation_FindAllAsync_System_String_" data-raw-source="[&lt;strong&gt;FindAllAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation#Windows_Devices_Enumeration_DeviceInformation_FindAllAsync_System_String_)"><strong>FindAllAsync</strong></a> 并获取设备的 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation" data-raw-source="[&lt;strong&gt;DeviceInformation&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation)"><strong>DeviceInformation</strong></a> 对象。</p>
<p>有关详细信息，请参阅 <a href="https://docs.microsoft.com/previous-versions/windows/apps/hh872189(v=win.10)" data-raw-source="[Quickstart: enumerating commonly used devices](https://docs.microsoft.com/previous-versions/windows/apps/hh872189(v=win.10))">快速入门：枚举常用设备</a>。</p></li>
<li>通过使用 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceWatcher" data-raw-source="[&lt;strong&gt;DeviceWatcher&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceWatcher)"><strong>DeviceWatcher</strong></a> 对象来检测何时将设备添加到系统或从系统中删除设备。
<ol>
<li>将 AQS 传递到 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation#Windows_Devices_Enumeration_DeviceInformation_CreateWatcher" data-raw-source="[&lt;strong&gt;CreateWatcher&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation#Windows_Devices_Enumeration_DeviceInformation_CreateWatcher)"><strong>CreateWatcher</strong></a> 并获取 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceWatcher" data-raw-source="[&lt;strong&gt;DeviceWatcher&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceWatcher)"><strong>DeviceWatcher</strong></a> 对象。</li>
<li>在 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceWatcher" data-raw-source="[&lt;strong&gt;DeviceWatcher&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceWatcher)"><strong>DeviceWatcher</strong></a> 对象上注册事件处理程序。</li>
<li>在<a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceWatcher#Windows_Devices_Enumeration_DeviceWatcher_Added" data-raw-source="[&lt;strong&gt;Added&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceWatcher#Windows_Devices_Enumeration_DeviceWatcher_Added)"><strong>添加</strong></a>的事件处理程序中获取设备的<a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation" data-raw-source="[&lt;strong&gt;DeviceInformation&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation)"><strong>DeviceInformation</strong></a>对象。</li>
<li>启动和停止 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceWatcher" data-raw-source="[&lt;strong&gt;DeviceWatcher&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceWatcher)"><strong>DeviceWatcher</strong></a> 对象。</li>
</ol>
有关详细信息，请参阅 <a href="https://docs.microsoft.com/previous-versions/windows/apps/hh967756(v=win.10)" data-raw-source="[How to get notifications if devices are added, removed, or changed](https://docs.microsoft.com/previous-versions/windows/apps/hh967756(v=win.10))">如何在添加、删除或更改设备时获取通知</a>。</li>
</ul></li>
<li>从 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation#Windows_Devices_Enumeration_DeviceInformation_Id" data-raw-source="[&lt;strong&gt;DeviceInformation.Id&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation#Windows_Devices_Enumeration_DeviceInformation_Id)"><strong>DeviceInformation.Id</strong></a> 属性获取设备实例。</li>
<li>通过传递设备实例字符串并获取<a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice" data-raw-source="[&lt;strong&gt;UsbDevice&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice)"><strong>UsbDevice</strong></a>对象来调用<a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_FromIdAsync_System_String_" data-raw-source="[&lt;strong&gt;FromIdAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_FromIdAsync_System_String_)"><strong>FromIdAsync</strong></a> 。</li>
</ol>
<p><strong>在示例中找到它：</strong> 请参阅名为 Scenario1_DeviceConnect 的文件。</p></td>
</tr>
<tr class="odd">
<td><a href="" id="step7"></a>
<p><strong>步骤 7</strong> (建议) -研究 <a href="usb-device-layout.md" data-raw-source="[USB device layout](usb-device-layout.md)">USB 设备布局</a>。</p></td>
<td><p>查看有关配置设备和执行数据传输的基本 USB 概念： <a href="usb-concepts-for-all-developers.md" data-raw-source="[Concepts for all USB developers](usb-concepts-for-all-developers.md)">所有 usb 开发人员的概念</a>。</p>
<p>查看设备配置描述符、每个受支持的备用设置及其终结点描述符的接口描述符。 通过使用 <a href="https://go.microsoft.com/fwlink/p/?linkid=617721" data-raw-source="[USBView](https://go.microsoft.com/fwlink/p/?linkid=617721)">USBView</a>，你可以浏览所有 usb 控制器和连接到它们的 usb 设备，还可以检查设备配置。</p></td>
</tr>
<tr class="even">
<td><a href="" id="step8"></a>
<p><strong>步骤 8</strong>-扩展应用程序以在 UI 中获取和显示 USB 描述符。</p></td>
<td><p><strong>快速入门：</strong> <a href="how-to-get-usb-descriptors--uwp-app-.md" data-raw-source="[How to get USB descriptors (UWP app)](how-to-get-usb-descriptors--uwp-app-.md)">如何获取 UWP 应用 (的 USB 描述符) </a></p>
<p></p>
<ul>
<li>通过获取 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor" data-raw-source="[&lt;strong&gt;UsbDevice.DeviceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor)"><strong>UsbDevice. DeviceDescriptor</strong></a> 值获取设备描述符。</li>
<li>获取 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_ConfigurationDescriptor" data-raw-source="[&lt;strong&gt;UsbConfiguration.ConfigurationDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_ConfigurationDescriptor)"><strong>UsbConfiguration.ConfigurationDescriptor</strong></a> 值，获取配置描述符。
<ul>
<li>通过获取 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors" data-raw-source="[&lt;strong&gt;UsbConfiguration.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors)"><strong>UsbConfiguration</strong></a> 属性获取完整的配置描述符集。</li>
</ul></li>
<li>获取 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_UsbInterfaces" data-raw-source="[&lt;strong&gt;UsbConfiguration.UsbInterfaces&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_UsbInterfaces)"><strong>UsbConfiguration UsbInterfaces</strong></a> 属性，获取配置中的接口数组。</li>
<li>通过获取 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_InterfaceSettings" data-raw-source="[&lt;strong&gt;UsbInterface.InterfaceSettings&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_InterfaceSettings)"><strong>InterfaceSettings</strong></a>获取备用设置的数组。</li>
<li><p>在活动的备用设置中，枚举管道并获取关联的终结点。</p>
<p>终结点描述符由以下对象表示：</p>
<ul>
<li><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInEndpointDescriptor" data-raw-source="[&lt;strong&gt;UsbBulkInEndpointDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInEndpointDescriptor)"><strong>UsbBulkInEndpointDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutEndpointDescriptor" data-raw-source="[&lt;strong&gt;UsbBulkOutEndpointDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutEndpointDescriptor)"><strong>UsbBulkOutEndpointDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInEndpointDescriptor" data-raw-source="[&lt;strong&gt;UsbInterruptInEndpointDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInEndpointDescriptor)"><strong>UsbInterruptInEndpointDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutEndpointDescriptor" data-raw-source="[&lt;strong&gt;UsbInterruptOutEndpointDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutEndpointDescriptor)"><strong>UsbInterruptOutEndpointDescriptor</strong></a></li>
</ul></li>
</ul>
<p><strong>在示例中找到它：</strong> 请参阅名为 Scenario5_UsbDescriptors 的文件。</p></td>
</tr>
<tr class="odd">
<td><a href="" id="step9"></a>
<p><strong>步骤 9</strong>-扩展应用程序以发送供应商定义的 USB 控制传输。</p></td>
<td><p><strong>快速入门：</strong> <a href="how-to-send-a-usb-control-transfer--uwp-app-.md" data-raw-source="[How to send a USB control transfer request (UWP app)](how-to-send-a-usb-control-transfer--uwp-app-.md)">如何将 USB 控件传输请求发送 (UWP 应用) </a></p>
<p></p>
<ol>
<li>从设备的硬件规范获取供应商命令。</li>
<li>创建 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbSetupPacket" data-raw-source="[&lt;strong&gt;UsbSetupPacket&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbSetupPacket)"><strong>UsbSetupPacket</strong></a> 对象，并通过设置各种属性填充安装包。</li>
<li>根据传输方向，启动异步操作以按这些方法发送控件传输：
<ul>
<li><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlInTransferAsync_Windows_Devices_Usb_UsbSetupPacket_Windows_Storage_Streams_IBuffer_" data-raw-source="[&lt;strong&gt;SendControlInTransferAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlInTransferAsync_Windows_Devices_Usb_UsbSetupPacket_Windows_Storage_Streams_IBuffer_)"><strong>SendControlInTransferAsync</strong></a></li>
<li><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_" data-raw-source="[&lt;strong&gt;SendControlOutTransferAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_)"><strong>SendControlOutTransferAsync</strong></a></li>
</ul></li>
</ol>
<p><strong>在示例中找到它：</strong> 请参阅名为 Scenario2_ControlTransfer 的文件。</p></td>
</tr>
<tr class="even">
<td><a href="" id="step10"></a>
<p><strong>步骤 10</strong>-扩展应用程序以读取或写入大容量数据。</p></td>
<td><p><strong>快速入门：</strong> <a href="how-to-send-a-usb-bulk-transfer--uwp-app-.md" data-raw-source="[How to send a USB bulk transfer request (UWP app)](how-to-send-a-usb-bulk-transfer--uwp-app-.md)">如何将 USB 批量传输请求发送 (UWP 应用) </a></p>
<p></p>
<ol>
<li> (<a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe" data-raw-source="[&lt;strong&gt;UsbBulkOutPipe&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe)"><strong>UsbBulkOutPipe</strong></a> 或 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe" data-raw-source="[&lt;strong&gt;UsbBulkInPipe&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe)"><strong>UsbBulkInPipe</strong></a>) 获取大容量管道对象。</li>
<li>配置批量管道以设置策略参数。</li>
<li>使用 <a href="https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataReader" data-raw-source="[&lt;strong&gt;DataReader&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataReader)"><strong>DataReader</strong></a> 或 <a href="https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataWriter" data-raw-source="[&lt;strong&gt;DataWriter&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataWriter)"><strong>DataWriter</strong></a> 对象设置数据流。</li>
<li>通过调用 <a href="https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataReader#Windows_Storage_Streams_DataReader_LoadAsync_System_UInt32_" data-raw-source="[&lt;strong&gt;DataReader.LoadAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataReader#Windows_Storage_Streams_DataReader_LoadAsync_System_UInt32_)"><strong>LoadAsync</strong></a> 或 <a href="https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataWriter#Windows_Storage_Streams_DataWriter_StoreAsync" data-raw-source="[&lt;strong&gt;DataWriter.StoreAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataWriter#Windows_Storage_Streams_DataWriter_StoreAsync)"><strong>DataWriter</strong></a>来启动异步传输操作。</li>
<li>获取传输操作的结果。</li>
</ol>
<p><strong>在示例中找到它：</strong> 请参阅名为 Scenario4_BulkPipes 的文件。</p></td>
</tr>
<tr class="odd">
<td><a href="" id="step11"></a>
<p><strong>步骤 11</strong>-扩展应用程序以获取硬件中断数据。</p></td>
<td><p><strong>快速入门：</strong> <a href="how-to-send-a-usb-interrupt-transfer--uwp-app-.md" data-raw-source="[How to send a USB interrupt transfer request (UWP app)](how-to-send-a-usb-interrupt-transfer--uwp-app-.md)">如何将 USB 中断传输请求发送 (UWP 应用) </a></p>
<p></p>
<ol>
<li> (<a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe" data-raw-source="[&lt;strong&gt;UsbInterruptInPipe&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe)"><strong>UsbInterruptInPipe</strong></a> 或 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe" data-raw-source="[&lt;strong&gt;UsbInterruptOutPipe&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe)"><strong>UsbInterruptOutPipe</strong></a>) 获取中断管道对象。</li>
<li>实现 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe#Windows_Devices_Usb_UsbInterruptInPipe_DataReceived" data-raw-source="[&lt;strong&gt;DataReceived&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe#Windows_Devices_Usb_UsbInterruptInPipe_DataReceived)"><strong>DataReceived</strong></a> 事件的中断处理程序。</li>
<li>注册事件处理程序以开始接收数据。</li>
<li>取消注册事件处理程序以停止接收数据。</li>
</ol>
<p><strong>在示例中找到它：</strong> 请参阅名为 Scenario3_InterruptPipes 的文件。</p></td>
</tr>
<tr class="even">
<td><a href="" id="step12"></a>
<p><strong>步骤 12</strong>-扩展应用以选择当前处于非活动状态的接口设置。</p></td>
<td><p><strong>快速入门：</strong> <a href="how-to-select-a-usb-interface-setting--uwp-app-.md" data-raw-source="[How to select a USB interface setting (UWP app)](how-to-select-a-usb-interface-setting--uwp-app-.md)">如何选择 (UWP 应用的 USB 接口设置) </a></p>
<p>当打开设备进行通信时，将选择默认接口及其第一个设置。 如果要更改该设置，请执行以下步骤：</p>
<ol>
<li>使用 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_Selected" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting.Selected&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_Selected)"><strong>UsbInterfaceSetting</strong></a> 值获取 USB 接口的活动设置。</li>
<li>通过调用 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_SelectSettingAsync" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting.SelectSettingAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_SelectSettingAsync)"><strong>UsbInterfaceSetting</strong></a>来启动异步操作，设置 USB 接口设置。</li>
</ol></td>
</tr>
<tr class="odd">
<td><a href="" id="step13"></a>
<p><strong>步骤 13</strong>-关闭设备。</p></td>
<td><p><strong>快速入门：</strong> <a href="how-to-connect-to-a-usb-device--uwp-app-.md" data-raw-source="[How to connect to a USB device (UWP app)](how-to-connect-to-a-usb-device--uwp-app-.md)">如何连接到 USB 设备 (UWP 应用) </a></p>
<p>使用完 UsbDevice 对象后，请关闭该设备。</p>
<p>C + + 应用程序必须使用 <strong>delete</strong> 关键字发布引用。 C #/VB 应用程序必须调用 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_Dispose" data-raw-source="[&lt;strong&gt;UsbDevice.Dispose&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_Dispose)"><strong>UsbDevice</strong></a> 方法。 JavaScript 应用程序必须调用 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_Close" data-raw-source="[&lt;strong&gt;UsbDevice.Close&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_Close)"><strong>UsbDevice</strong></a>。</p>
<p><strong>在示例中找到它：</strong> 请参阅名为 Scenario1_DeviceConnect 的文件。</p></td>
</tr>
<tr class="even">
<td><a href="" id="step14"></a>
<p><strong>步骤 14</strong>-为应用创建设备元数据包。</p></td>
<td><strong>工具：</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/device-metadata-authoring-wizard-portal" data-raw-source="[Device Metadata Authoring Wizard](https://docs.microsoft.com/windows-hardware/drivers/devtest/device-metadata-authoring-wizard-portal)">设备元数据创作向导</a>
<ul>
<li>如果已安装 Windows 驱动程序工具包 (WDK) ，请打开 <strong>驱动程序</strong> &gt; <strong>设备元数据</strong> &gt; <strong>创作</strong>。</li>
<li>如果已安装独立 SDK，则该工具位于<em> &lt; install_path &gt; </em>\bin\x86\DeviceMetadataWizardexe。</li>
</ul>
<p>按照向导中的步骤，将应用程序与设备相关联。 输入有关设备的以下信息：</p>
<p></p>
<ul>
<li>在 " <strong>设备信息</strong> " 页上，输入 " <strong>型号名称</strong>"、" <strong>制造商</strong>" 和 " <strong>说明</strong>"。</li>
<li>在 " <strong>硬件信息</strong> " 页上，输入设备的硬件 ID。</li>
</ul>
<p><strong>若要将应用声明为设备的特权应用，请按照以下说明操作：</strong></p>
<ol>
<li><p>在 " <strong>应用程序信息</strong> " 页上的 " <strong>特权应用程序</strong> " 组中，输入 <strong>包名称</strong>、 <strong>发布者名称</strong>和 <strong>UWP 应用 ID</strong>。</p>
<p><img src="images/privileged-app.png" alt="device metatdata for privileged apps" /></p>
<div class="alert">
<strong>注意</strong>   不要检查<strong>Access 自定义驱动程序</strong>选项。
</div>
<div>
 
</div></li>
<li>打开 " <strong>完成</strong> " 选项卡。选中 "将 <strong>包复制到系统的本地元数据存储</strong> " 复选框。</li>
<li>连接设备，在 "控制面板" 中，打开 " <strong>查看设备和打印机</strong> " 并验证设备的图标是否正确。</li>
</ol>
<p><strong>在示例中找到它：</strong> 请参阅 DeviceMetadata 文件夹。</p></td>
</tr>
<tr class="odd">
<td><a href="" id="step15"></a>
<p><strong>步骤 15</strong>-扩展应用程序以实现自动播放激活，以便在设备连接到系统时启动应用。</p></td>
<td><p><strong>快速入门：</strong> <a href="https://docs.microsoft.com/previous-versions/windows/apps/jj161017(v=win.10)" data-raw-source="[Register an app for an AutoPlay device](https://docs.microsoft.com/previous-versions/windows/apps/jj161017(v=win.10))">为自动播放设备注册应用</a></p>
<p>可以添加自动播放功能，以便在设备连接到系统时启动应用。 可以 (特权或其他) 为所有 UWP 应用启用自动播放。</p>
<p></p>
<ol>
<li>在设备元数据包中，必须指定设备应如何响应自动播放通知。 在 " <strong>Windows 信息</strong> " 选项卡上，选择 " <strong>UWP 设备应用</strong> " 选项，然后输入应用信息，如下所示：</li>
<li><p>在应用程序清单中，添加 <strong>自动播放设备</strong> 声明和启动信息，如下所示：</p>
<p><img src="images/autoplay.png" alt="AutoPlay" /></p></li>
<li>在 App 类的 OnActivated 方法中，检查设备是否激活了该应用。 如果是，则该方法接收包含 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation#Windows_Devices_Enumeration_DeviceInformation_Id" data-raw-source="[&lt;strong&gt;DeviceInformation.Id&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation#Windows_Devices_Enumeration_DeviceInformation_Id)"><strong>DeviceInformation.Id</strong></a> 属性值的 DeviceEventArgs 参数值。 这与步骤6中所述的值相同<a href="#step6" data-raw-source="[&lt;strong&gt;Step 6&lt;/strong&gt;—Extend the app to open the device for communication](#step6)"> <strong>Step 6</strong>，即扩展应用程序以打开设备进行通信</a>。</li>
</ol>
<p><strong>在示例中找到它：</strong> 查看名为自动播放的文件。 有关 JavaScript，请参阅 default.js。</p></td>
</tr>
<tr class="even">
<td><a href="" id="step16"></a>
<p><strong>步骤 16</strong>：扩展应用程序以实现可执行到设备的长度传输的后台任务，例如固件更新，不会使应用挂起。</p></td>
<td><p>若要实现后台任务，需要两个类。</p>
<p>后台任务类实现 <a href="https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.IBackgroundTask" data-raw-source="[&lt;strong&gt;IBackgroundTask&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.IBackgroundTask)"><strong>IBackgroundTask</strong></a> 接口，并包含您创建的用于同步或更新外围设备的实际代码。 当后台任务触发时，将执行后台任务类，并从应用程序的应用程序清单中提供的入口点执行。</p>
<div class="alert">
<strong>注意</strong>  Windows 8.1 提供的设备后台任务基础结构。 有关 Windows 后台任务的详细信息，请参阅 <a href="https://docs.microsoft.com/previous-versions/windows/apps/hh977056(v=win.10)" data-raw-source="[Supporting your app with background tasks](https://docs.microsoft.com/previous-versions/windows/apps/hh977056(v=win.10))">支持包含后台任务的应用</a>。
</div>
<div>
 
</div>
<p><strong>后台任务类</strong></p>
<ol>
<li>实现 Windows 后台任务基础结构所需的 <a href="https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.IBackgroundTask" data-raw-source="[&lt;strong&gt;IBackgroundTask&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.IBackgroundTask)"><strong>IBackgroundTask</strong></a> 接口。</li>
<li>获取传递给 <strong>Run</strong> 方法中的类的 DeviceUseDetails 实例，并使用此实例将进度报告回 Microsoft Store 应用并注册取消事件。</li>
<li><strong>Run</strong>方法还会调用实现后台设备同步代码的私有 OpenDevice 和 WriteToDeviceAsync 方法。</li>
</ol>
<p>UWP 应用注册并触发 DeviceUseTrigger 后台任务。 应用在后台任务上注册、触发和处理进度。</p>
<div class="alert">
<strong>注意</strong>   下面的示例代码可以通过使用相应的对象应用到 DeviceServicingTrigger 后台任务。 这两个触发器对象及其对应的 Api 的唯一区别是 Windows 进行的策略检查。
</div>
<div>
 
</div>
<ol>
<li>创建 DeviceUseTrigger 和 BackgroundTaskRegistration 对象。</li>
<li>检查此示例应用程序以前是否已注册了任何后台任务，并通过对任务调用 "取消注册" 方法来取消它们。</li>
<li>注册要与设备同步的后台任务。 在下一步中，从 SyncWithDeviceAsync 方法调用 SetupBackgroundTask 方法。
<ol>
<li>初始化 DeviceUseTrigger 并将其保存供以后使用。</li>
<li>创建一个 BackgroundTaskBuilder 对象，并使用其名称、TaskEntryPoint 和 SetTrigger 属性和方法来注册应用程序的 DeviceUseTrigger 对象和后台任务名称。 BackgroundTaskBuilder 对象的 TaskEntryPoint 属性设置为触发后台任务时要运行的后台任务类的全名。</li>
<li>在后台任务中注册完成和进度事件，以便 Microsoft Store 应用程序可以为用户提供完成和进度更新。</li>
</ol></li>
<li>Private SyncWithDeviceAsync 方法注册将与设备同步的后台任务，并启动后台同步。
<ol>
<li>调用上一步中的 SetupBackgroundTask 方法，并注册将与设备同步的后台任务。</li>
<li>调用专用的 StartSyncBackgroundTaskAsync 方法，该方法可启动后台任务。</li>
<li>将应用程序的句柄关闭到设备，以确保后台任务在启动时能够打开设备。
<div class="alert">
<strong>注意</strong>   后台任务需要打开设备以执行更新，以便 Microsoft Store 应用必须在调用 RequestAsync 之前关闭与设备的连接
</div>
<div>
 
</div></li>
<li>调用 DeviceUseTrigger 对象的 RequestAsync 方法，该方法可启动后台任务并返回 RequestAsync 中的 DeviceTriggerResults 对象，该对象用于确定是否成功启动了后台任务。
<div class="alert">
<strong>注意</strong>   Windows 将进行检查以确保所有必要的任务启动策略检查已完成。 如果所有策略检查都已完成，则更新操作现在将作为 Microsoft Store 应用外部的后台任务运行，从而允许在操作正在进行时安全挂起应用。 如果不再满足这些要求，Windows 还将强制实施任何运行时要求并取消后台任务。
</div>
<div>
 
</div></li>
<li>使用从 StartSyncBackgroundTaskAsync 返回的 DeviceTriggerResults 对象来确定后台任务是否成功启动。 Switch 语句用于检查 DeviceTriggerResults 的结果。</li>
</ol></li>
<li>实现一个私有 OnSyncWithDeviceProgress 事件处理程序，该处理程序将使用后台任务的进度更新应用程序 UI。</li>
<li>实现私有 OnSyncWithDeviceCompleted 事件处理程序，以便在后台任务完成后处理从后台任务过渡到前台应用的操作。
<ol>
<li>使用 BackgroundTaskCompletedEventArgs 对象的 CheckResults 方法来确定由后台任务引发的任何异常。</li>
<li>应用程序重新打开设备供前台应用程序使用，现在后台任务已完成，并更新 UI 以通知用户。</li>
</ol></li>
<li>实现专用按钮单击 UI 中的事件处理程序以启动和取消后台任务。
<ol>
<li>Private Sync_Click 事件处理程序调用前面步骤中描述的 SyncWithDeviceAsync 方法。</li>
<li>Private CancelSync_Click 事件处理程序调用私有 CancelSyncWithDevice 方法来取消后台任务。</li>
</ol></li>
<li>Private CancelSyncWithDevice 方法取消注册并取消任何活动设备同步，以便可以使用 BackgroundTaskRegistration 对象上的 "取消注册" 方法重新打开设备。</li>
</ol>
<p><strong>在示例中找到它：</strong> 请参阅名为 Scenario7_Sync 文件的文件。 在 IoSyncBackgroundTask 中实现了后台类。</p></td>
</tr>
<tr class="odd">
<td><a href="" id="step17"></a>
<p><strong>步骤 17</strong>-运行 Windows 应用认证工具包。</p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/apps/hh694081(v=win.10)" data-raw-source="[Using the Windows App Certification Kit](https://docs.microsoft.com/previous-versions/windows/apps/hh694081(v=win.10))">使用 Windows 应用程序认证工具包</a></p>
<p>推荐。 运行 Windows 应用程序认证包可帮助你确保你的应用程序满足 Microsoft Store 要求，因此，在你将主要功能添加到应用程序时，应执行此操作。</p></td>
</tr>
</tbody>
</table>

 

## <a name="want-to-know-more"></a>想要了解更多信息？


详细了解相关示例。

**相关示例**

-   [USB CDC 控制示例](https://go.microsoft.com/fwlink/p/?linkid=309716)
-   [固件更新 USB 设备示例](https://go.microsoft.com/fwlink/p/?linkid=309716)

[UWP 应用 UI，开始 (XAML) ](https://docs.microsoft.com/previous-versions/windows/apps/dn263191(v=win.10))

详细了解如何设计 UWP 应用 UI。

使用[c # 和 Visual Basic 的 uwp 应用](https://docs.microsoft.com/previous-versions/windows/apps/br229583(v=win.10))和[使用 c + + 的 uwp 应用路线图](https://docs.microsoft.com/previous-versions/windows/apps/hh700360(v=win.10))的路线图

详细了解如何使用 c + +、c # 或 Visual Basic 来创建 UWP 应用。

[异步编程（UWP 应用）](https://docs.microsoft.com/previous-versions/windows/apps/hh464924(v=win.10))

了解如何使你的应用程序在执行可能需要较长时间的操作时保持响应。

 

 




