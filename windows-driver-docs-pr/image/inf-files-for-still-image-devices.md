---
title: 静止图像设备 INF 文件
description: 静止图像设备 INF 文件
ms.assetid: f68ba904-9049-4f7e-9903-fdf6f413a1a5
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: d8f2db18b4d7e901bcce1e4164d88c548ef55c5d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525542"
---
# <a name="inf-files-for-still-image-devices"></a>静止图像设备 INF 文件

静止图像设备的默认类安装程序*sti\_ci.dll*，可以识别一组特殊的 INF 文件条目。 在 INF 文件中，这些项必须放置在设备的[ **INF DDInstall 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)。 下表所述的条目。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>INF 文件条目</th>
<th>值</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>SubClass</strong></p></td>
<td><p><strong>StillImage</strong></p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceType</strong></p></td>
<td><p><strong>1</strong>扫描仪，对于<strong>2</strong>用于相机， <strong>3</strong>视频设备</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceSubType</strong></p></td>
<td><p>供应商定义的值。</p></td>
<td><p>可选</p></td>
</tr>
<tr class="even">
<td><p><strong>连接</strong></p></td>
<td><p>对于非 PnP 设备连接到串行或并行端口，这可能是<strong>串行</strong>或<strong>并行</strong>若要限制用户&#39;s 选择的在安装过程中的端口。</p></td>
<td><p>可选。 如果未指定，则用户可以选择任何串行或并行端口。</p></td>
</tr>
<tr class="odd">
<td><p><strong>功能</strong></p></td>
<td><p>指定一个数字，将转换为位标志识别设备功能。 这些标志在注册表中存储和适用于通过 Microsoft STI 组件<a href="https://msdn.microsoft.com/library/windows/hardware/ff548380" data-raw-source="[&lt;strong&gt;STI_DEV_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548380)"> <strong>STI_DEV_CAPS</strong> </a>结构。</p>
<p>位 0 − 集/清除 STI_GENCAP_NOTIFICATIONS STI_DEV_CAPS 中。</p>
<p>位 1 − 集/清除 STI_GENCAP_POLLING_NEEDED STI_DEV_CAPS 中。</p>
<p>位 2 − 集/清除 STI_GENCAP_GENERATE_ARRIVALEVENT STI_DEV_CAPS 中。</p>
<p>位 3 − 集/清除 STI_GENCAP_AUTO_PORTSELECT STI_DEV_CAPS 中。</p></td>
<td><p>可选</p></td>
</tr>
<tr class="even">
<td><p><strong>PropertyPages</strong></p></td>
<td><p>标识一个 DLL，它会创建自定义的名称和入口点<a href="property-sheet-pages-for-still-image-devices.md" data-raw-source="[Property Sheet Pages for Still Image Devices](property-sheet-pages-for-still-image-devices.md)">静止图像设备的属性表页</a>。</p>
<p>下面的示例标识 DLL <em>estp2cpl.dll</em>，并将<strong>EnumStiPropPages</strong>此 DLL 中的入口点。 入口点名称是可选的;如果省略，入口点默认为<strong>EnumStiPropPages</strong>。</p>
<pre space="preserve"><code>PropertyPages = estp2cpl.dll, EnumStiPropPages</code></pre></td>
<td><p>可选</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceData</strong></p></td>
<td><p>标识包含信息存储在注册表中下的供应商提供的数据部分<strong>DeviceData</strong>密钥。 对于 TWAIN 支持的设备，必须包含的数据部分<strong>TwainDS</strong>条目 (请参阅<a href="registry-entries-for-still-image-devices.md#ddk-vendor-modifiable-registry-values-si" data-raw-source="[Vendor-Modifiable Registry Values](registry-entries-for-still-image-devices.md#ddk-vendor-modifiable-registry-values-si)">供应商可修改的注册表值</a>)。</p></td>
<td><p>可选。 此项是必需的有关<a href="creating-push-model-aware-applications.md" data-raw-source="[Creating Push-Model Aware Applications](creating-push-model-aware-applications.md)">创建推送模型意识的应用程序</a>，但是。</p></td>
</tr>
<tr class="even">
<td><p><strong>事件</strong></p></td>
<td><p>标识某个供应商提供的数据部分列出了静止图像设备事件。 在本部分中的每个条目必须具有以下格式：</p>
<p><em>EventName</em><strong>=&quot;</strong><em>字符串</em><strong>&quot;，{</strong><em>GUID</em> <strong>}，</strong>应用</p>
<p><em>EventName</em>是事件&#39;s 内部名称，<em>字符串</em>事件&#39;s 显示字符串<em>GUID</em>是事件&#39;s GUID (请参阅<a href="still-image-device-events.md" data-raw-source="[Still Image Device Events](still-image-device-events.md)">仍映像设备事件</a>)，并<em>应用</em>指定在事件发生时启动的映像应用程序。 若要启动当前已注册的应用程序，请使用星号 (<strong>*</strong>) 用于<em>应用</em>。</p></td>
<td><p>可选。 此项是必需的有关<a href="creating-push-model-aware-applications.md" data-raw-source="[Creating Push-Model Aware Applications](creating-push-model-aware-applications.md)">创建推送模型意识的应用程序</a>，但是。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UninstallSection</strong></p></td>
<td><p>指向通常包含一个 INF 部分<a href="https://msdn.microsoft.com/library/windows/hardware/ff547363" data-raw-source="[&lt;strong&gt;INF DelFiles directives&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547363)"> <strong>INF DelFiles 指令</strong></a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff547374" data-raw-source="[&lt;strong&gt;INF DelReg directives&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547374)"> <strong>INF DelReg 指令</strong></a>。 在本部分中的条目采用以下格式：</p>
<p><strong>UninstallSection</strong><em>=UninstallSectionName</em></p>
<p><em>UninstallSectionName</em>的节，其中包含名称<strong>Delfiles</strong>或<strong>DelReg</strong>指令。 请注意该 Windows 文件保护 (<a href="https://msdn.microsoft.com/library/windows/hardware/ff556347#wdkgloss-windows-file-protection--wfp-" data-raw-source="&lt;em&gt;Windows File Protection (WFP)&lt;/em&gt;"><em>Windows 文件保护 (WFP)</em></a>) 可能会禁止用户删除一些文件，即使它们使用指定<strong>DelFiles</strong>指令。</p></td>
<td><p>可选。 此项是仅对 Windows 2000 有效。</p></td>
</tr>
</tbody>
</table>

静止图像设备的默认类安装程序支持标准[ **INF CopyFiles 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546346)。 安装程序使用内部引用计数器组件文件，因此，由多个设备共享的文件不会删除过早卸载操作的过程。

静止图像设备，默认 INF 文件*sti.inf*，定义每个设备类型，两个安装部分，如下所示：

- [ **INF DDInstall 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)，其中必须引用内*DDInstall*供应商提供 INF 文件中的以下表所示的部分。

    <table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>有关 USB 设备</th>
    <th>SCSI 设备</th>
    <th>对于串行设备</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><pre space="preserve"><code>Include=sti.inf</code></pre>
    <pre space="preserve"><code>Needs=STI.USBSection</code></pre></td>
    <td><pre space="preserve"><code>Include=sti.inf</code></pre>
    <pre space="preserve"><code>Needs=STI.SCSISection</code></pre></td>
    <td><pre space="preserve"><code>Include=sti.inf</code></pre>
    <pre space="preserve"><code>Needs=STI.SerialSection</code></pre></td>
    </tr>
    </tbody>
    </table>

- [ **INF DDInstall.Services 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547349)，其中必须引用内*DDInstall*。**服务**供应商提供 INF 文件中的以下表所示的部分。

    <table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>有关 USB 设备</th>
    <th>SCSI 设备</th>
    <th>对于串行设备</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><pre space="preserve"><code>Include=sti.inf</code></pre>
    <pre space="preserve"><code>Needs=STI.USBSection.Services</code></pre></td>
    <td><pre space="preserve"><code>Include=sti.inf</code></pre>
    <pre space="preserve"><code>Needs=STI.SCSISection.Services</code></pre></td>
    <td><pre space="preserve"><code>Include=sti.inf</code></pre>
    <pre space="preserve"><code>Needs=STI.SerialSection.Services</code></pre></td>
    </tr>
    </tbody>
    </table>

如果你还[创建图像采集 Api 的特定于设备的组件](creating-device-specific-components-for-image-acquisition-apis.md)，通常将 INF 文件中包括这些组件的文件名。

有关创建静止图像设备的 INF 文件中的其他指南，你可以查看任何与包含的项的 Windows 提供的 INF 文件"子类 = StillImage"。

## <a name="remarks"></a>备注

当开发用于扫描程序的 INF 文件后时，可以使用[Microsoft OS 描述符](https://msdn.microsoft.com/library/windows/hardware/gg463179.aspx)启用兼容性 ID 功能。 当执行此操作时，允许一个扫描程序驱动程序与多个扫描程序模型兼容。
