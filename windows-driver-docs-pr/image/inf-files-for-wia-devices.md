---
title: WIA 设备 INF 文件
description: WIA 设备 INF 文件
ms.assetid: 65eac8b5-35d2-4537-8646-a35a1cf9aced
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 807c9a58687c6fb602f1f2eb45035c42c58b775a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521860"
---
# <a name="inf-files-for-wia-devices"></a>WIA 设备 INF 文件


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
<td><p>StillImage</p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceType</strong></p></td>
<td><p>扫描程序的 1</p>
<p>用于相机的 2</p>
<p>流式处理视频 3</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceSubType</strong></p></td>
<td><p>供应商定义的值</p></td>
<td><p>可选</p></td>
</tr>
<tr class="even">
<td><p><strong>连接</strong></p></td>
<td><p>对于非即插连接到串行或并行端口设备，这可能是串行或并行，以限制用户&#39;s 选择的在安装过程中的端口。</p></td>
<td><p>可选</p>
<p>如果未指定，则用户可以选择任何串行或并行端口。</p></td>
</tr>
<tr class="odd">
<td><p><strong>功能</strong></p></td>
<td><p>指定一个数字，将转换为位标志识别设备功能。 这些标志在注册表中存储并且通过 STI_DEV_CAPS 结构 STI 组件可用的。</p>
<p>位 0 − 集/清除 STI_GENCAP_NOTIFICATIONS STI_DEV_CAPS 中。</p>
<p>位 1 − 集/清除 STI_GENCAP_POLLING_NEEDED STI_DEV_CAPS 中。</p>
<p>位 2 − 集/清除 STI_GENCAP_GENERATE_ARRIVALEVENT STI_DEV_CAPS 中。</p>
<p>位 3 − 集/清除 STI_GENCAP_AUTO_PORTSELECT STI_DEV_CAPS 中。</p>
<p>位 4 − 集/清除 STI_GENCAP_WIA STI_DEV_CAPS 中。</p>
<p>位 5 − 集/清除 STI_GENCAP_SUBSET STI_DEV_CAPS 中。</p></td>
<td><p>可选</p>
<p>当前未使用 5 位。</p>
<p>将此条目设置为 0x33 以与您的扫描仪支持按钮式事件 INF 文件中。</p></td>
</tr>
<tr class="even">
<td><p><strong>PropertyPages</strong></p></td>
<td><p>用于 Windows 98 和 Windows 2000 仅</p>
<p>标识创建为静止图像设备的自定义的属性表页的 DLL 的名称和入口点。</p>
<p>有关详细信息<strong>属性页</strong>条目，请参阅<a href="inf-files-for-still-image-devices.md" data-raw-source="[INF Files for Still Image Devices](inf-files-for-still-image-devices.md)">仍映像设备 INF 文件</a>。</p></td>
<td><p>可选</p>
<p>此条目是以仅供 STI 驱动程序和已过时 WIA 的驱动程序。</p>
<p>有关与 WIA 驱动程序开发人员相关的属性页的信息，请参阅<strong>注意</strong>此表后面的属性页上。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceData</strong></p></td>
<td><p>标识包含信息存储在注册表中下的供应商提供的数据部分<strong>DeviceData</strong>密钥。 TWAIN 支持的设备，对于数据部分必须包含 TwainDS 条目 (请参阅<a href="registry-entries-for-wia-drivers.md" data-raw-source="[Registry Entries for WIA Drivers](registry-entries-for-wia-drivers.md)">WIA 驱动程序的注册表项</a>)。</p></td>
<td><p>可选</p></td>
</tr>
<tr class="even">
<td><p><strong>事件</strong></p></td>
<td><p>标识某个供应商提供的数据部分列出了静止图像设备事件。 在本部分中的每个条目必须具有以下格式：</p>
<p><em>EventName</em><strong>=&quot;</strong><em>字符串</em><strong>&quot;，{</strong><em>GUID</em> <strong>}，</strong>应用</p>
<p><em>EventName</em>是事件&#39;s 内部名称，<em>字符串</em>是事件&#39;s 显示字符串<em>GUID</em>是事件&#39;GUID，s 和<em>应用</em>指定要在事件发生时启动映像的应用程序。 若要启动当前已注册的应用程序，请使用星号 (<strong>*</strong>) 用于<em>应用</em>。</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p><strong>PortSelect</strong></p></td>
<td><p>如果设备安装不需要端口选择页上，值为&quot;没有&quot;导致跳过该页面。 此值还会导致<strong>CreateFileName</strong>条目值 (请参阅<strong>注意</strong>上<strong>CreateFileName</strong>并<strong>PortSelect</strong>参看此表) 以自动设置为自动。</p>
<p>要显示 Message1 会导致系统提供消息和设置的值<strong>CreateFileName</strong>条目值为自动。</p>
<p>适用于扫描仪和照相机需要手动安装。</p></td>
<td><p>可选</p>
<p>请注意，对于插设备<strong>PortSelect</strong>将被忽略，但设备仍必须具有<strong>CreateFileName</strong>项值设置为自动，才能 WIA 加载设备。 使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff546320" data-raw-source="[&lt;strong&gt;INF AddReg Directive&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546320)"> <strong>INF AddReg 指令</strong></a>添加到此条目<a href="https://msdn.microsoft.com/library/windows/hardware/ff547344" data-raw-source="[&lt;strong&gt;INF DDInstall Section&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547344)"> <strong>INF DDInstall 部分</strong></a>设备的&#39;s INF 文件。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  用户模式下客户端 （微型驱动程序） 必须以与设备通信，要求设备的文件的名称和一个字符串，指定要创建或打开的对象名称的 WIA 服务。 （文件名没有为磁盘文件的名称。）对此类查询的响应，WIA 服务获取来自设备的文件名**CreateFileName**注册表项。 ( *Usbscan.sys*并*scsiscan.sys*内核模式驱动程序创建此条目中，类安装程序也一样。)微型驱动程序通过调用接收此文件的名称[ **IStiDeviceControl::GetMyDevicePortName** ](https://msdn.microsoft.com/library/windows/hardware/ff542944)方法。 调用时，微型驱动程序然后可以使用此文件的名称[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)函数 （Microsoft Windows SDK 文档中所述） 来打开设备的句柄。
如果手动安装该设备，类安装程序将创建**CreateFileName**项，将其值设置为一个依赖的端口选择页面上的用户的选项：COM*X*，LPT*X*，或 AUTO。 手动安装某些设备 （例如网络扫描仪） 不需要一个端口。 在这种情况下，生成的端口选择对话框可使用户感到困惑。 可以防止此对话框通过添加以下条目中的出现[ **INF DDInstall 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)的设备的 INF 文件：

 

```INF
     PortSelect=NO
```

**请注意**  此条目值的一个副作用是， **CreateFileName**条目将设置为自动。 请注意，如果微型驱动程序收到自动的文件名称，则它必须能够确定自身应与哪些设备。

**请注意**  的属性页，WIA 驱动程序必须使用不同的扩展机制，来添加属性页。 它还必须添加到其自己的 GUID **UI 类 ID**条目中相应的 INF 文件，并且必须提供特定 UI 扩展性注册 (请参阅[用户界面扩展插件注册表项](user-interface-extension-registry-entries.md)) 的 UI 组件正在替换，如公共对话框，或添加，如上下文菜单和属性页。 WIA 驱动程序还必须为组件本身提供 UI 扩展注册。

 

 

### <a name="additional-inf-file-entries"></a>其他的 INF 文件条目

下表中的条目必须指向通过设备的节中放置[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320):

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
<td><p><strong>HardwareConfig</strong></p></td>
<td><p>指示使用设备的连接类型。</p>
<p>1，1 − 通用 WDM 设备</p>
<p>1，2 − SCSI 设备</p>
<p>1，4 − USB 设备</p>
<p>1,8 − 串行设备</p>
<p>1,16 − 并行设备</p></td>
<td><p>可选</p></td>
</tr>
<tr class="even">
<td><p><strong>USDClass</strong></p></td>
<td><p>指示微型驱动程序的 GUID。</p></td>
<td><p>可选。</p>
<p>中的 GUID <strong>USDClass</strong>并<strong>CLSID</strong>条目必须匹配中使用的 GUID <strong>DllGetClassObject</strong>微型驱动程序的函数。 如果你正在编写 microdriver，值应为 BB6CF8E2-1511年-40bd-91BA-80D43C53064E。 否则，必须生成新的 GUID，使用，例如， <em>genguid.exe</em>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CLSID</strong></p></td>
<td><p>指示微型驱动程序的 GUID。</p></td>
<td><p>可选。</p>
<p>请参阅前面紧邻的注释<strong>USDClass</strong>条目。</p></td>
</tr>
</tbody>
</table>

 

静止图像设备的默认类安装程序支持标准[ **INF CopyFiles 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546346)。

静止图像设备，默认 INF 文件*sti.inf*，定义每个设备类型，两个安装部分，如下所示：

-   [ **INF DDInstall 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)，其中必须引用内*DDInstall*供应商提供 INF 文件中的以下表所示的部分。

    <table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>设备类型</th>
    <th>包括</th>
    <th>需求</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>IEEE 1394/SBP2</p></td>
    <td><p>Include=sti.inf</p></td>
    <td><p>Needs=STI.SBP2Section</p></td>
    </tr>
    <tr class="even">
    <td><p>USB</p></td>
    <td><p>Include=sti.inf</p></td>
    <td><p>需要 = STI。USBSection</p></td>
    </tr>
    <tr class="odd">
    <td><p>SCSI</p></td>
    <td><p>Include=sti.inf</p></td>
    <td><p>需要 = STI。SCSISection</p></td>
    </tr>
    <tr class="even">
    <td><p>序列</p></td>
    <td><p>Include=sti.inf</p></td>
    <td><p>Needs=STI.SerialSection</p></td>
    </tr>
    </tbody>
    </table>

     

<!-- -->

-   INF DDInstall 服务部分中，必须在引用[ **INF DDInstall.Services 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547349)的供应商提供的 INF 文件下, 表中所示。

    <table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>设备类型</th>
    <th>包括</th>
    <th>需求</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>1394/SBP2</p></td>
    <td><p>Include=sti.inf</p></td>
    <td><p>Needs=STI.SBP2Section.Services</p></td>
    </tr>
    <tr class="even">
    <td><p>USB</p></td>
    <td><p>Include=sti.inf</p></td>
    <td><p>Needs=STI.USBSection.Services</p></td>
    </tr>
    <tr class="odd">
    <td><p>SCSI</p></td>
    <td><p>Include=sti.inf</p></td>
    <td><p>Needs=STI.SCSISection.Services</p></td>
    </tr>
    <tr class="even">
    <td><p>序列</p></td>
    <td><p>Include=sti.inf</p></td>
    <td><p>Needs=STI.SerialSection.Services</p></td>
    </tr>
    </tbody>
    </table>

     

有关创建静止图像设备的 INF 文件中的其他指南，你可以查看任何与包含项子类的 Windows 提供的 INF 文件 = StillImage。

若要指定设备为 WIA 的设备，微型驱动程序 INF 文件必须包含以下值放在*DeviceData*供应商提供 INF 文件部分。

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
<td><p><strong>Server</strong></p></td>
<td><p>本地</p></td>
<td><p>将设备指定为本地设备。 这是可选的如果供应商未指定项值，该设备被假定为本地。 也就是说，WIA_DIP_SERVER_NAME 属性设置为本地。</p></td>
</tr>
<tr class="even">
<td><p><strong>MicroDriver</strong></p></td>
<td><p>供应商提供<em>.dll</em>文件名称</p></td>
<td><p>此条目应设置为实现 WIA microdriver 的供应商提供的 DLL 的名称。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UI DLL</strong></p></td>
<td><p>供应商提供<em>.dll</em>文件名称</p></td>
<td><p>过时，并永远不会使用。 以前，此条目表示供应商提供的用户界面的 DLL 文件的名称。</p></td>
</tr>
<tr class="even">
<td><p><strong>用户界面类 ID</strong></p></td>
<td><p>供应商提供的设备类标识符</p></td>
<td><p>指示设备的供应商提供的类用户界面能够支持。 这是可选的如果供应商未指定项值，WIA 将 WIA_DIP_UI_CLSID 属性设置为 GUID_NULL 和 WIA UI 使用的默认值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ICMProfiles</strong></p></td>
<td><p>供应商提供的颜色配置文件值</p></td>
<td><p>指定要放入 WIA_IPA_ICM_PROFILE_NAME 属性的值。 如果未不指定任何值，标准 sRGB 配置文件<em>sRGB 颜色空间 Profile.icm</em>使用。</p></td>
</tr>
</tbody>
</table>

 

**MicroDriver**项是必需的仅当由供应商提供 WIA microdriver。

仅当由供应商提供用于图像处理设备的自定义用户界面，用户界面 (UI) 项是必需的。

**备注**

当开发用于扫描程序的 INF 文件后时，可以使用[Microsoft OS 描述符](https://msdn.microsoft.com/library/windows/hardware/gg463179.aspx)启用兼容性 ID 功能。 当执行此操作时，允许一个扫描程序驱动程序与多个扫描程序模型兼容。

 

 




