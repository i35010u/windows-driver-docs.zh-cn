---
title: WIA 设备的 INF 文件
description: WIA 设备的 INF 文件
ms.assetid: 65eac8b5-35d2-4537-8646-a35a1cf9aced
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5ae7a1de6a227954ccd3b8b839683b67065581bb
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716404"
---
# <a name="inf-files-for-wia-devices"></a>WIA 设备的 INF 文件


静态映像设备的默认类安装程序 *sti \_ci.dll*可识别一组特殊的 INF 文件条目。 在 INF 文件中，这些条目必须位于设备的 [**INF DDInstall 部分**](../install/inf-ddinstall-section.md)中。 下表中描述了这些条目。

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
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>类别</strong></p></td>
<td><p>StillImage</p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceType</strong></p></td>
<td><p>1用于扫描仪</p>
<p>2照相机</p>
<p>3对于流式处理视频</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceSubType</strong></p></td>
<td><p>供应商定义的值</p></td>
<td><p>可选</p></td>
</tr>
<tr class="even">
<td><p><strong>Connection</strong></p></td>
<td><p>对于连接到串行端口或并行端口的非即插即用设备，这可能是串行或并行的，以限制用户在安装过程中选择的端口。</p></td>
<td><p>可选</p>
<p>如果未指定，则用户可以选择任何串行端口或并行端口。</p></td>
</tr>
<tr class="odd">
<td><p><strong>功能</strong></p></td>
<td><p>指定一个数字，该数字将转换为标识设备功能的位标志。 这些标志存储在注册表中，可通过 STI_DEV_CAPS 结构通过 STI 组件使用。</p>
<p>位0−设置/清除 STI_DEV_CAPS 中的 STI_GENCAP_NOTIFICATIONS。</p>
<p>第1位−设置/清除 STI_DEV_CAPS 中的 STI_GENCAP_POLLING_NEEDED。</p>
<p>第2位−设置/清除 STI_DEV_CAPS 中的 STI_GENCAP_GENERATE_ARRIVALEVENT。</p>
<p>第3位−设置/清除 STI_DEV_CAPS 中的 STI_GENCAP_AUTO_PORTSELECT。</p>
<p>Bit 4 −设置/清除 STI_DEV_CAPS 中的 STI_GENCAP_WIA。</p>
<p>位5−设置/清除 STI_DEV_CAPS 中的 STI_GENCAP_SUBSET。</p></td>
<td><p>可选</p>
<p>当前未使用位5。</p>
<p>将 INF 文件中的此项设置为0x33，以支持通过扫描仪进行推送按钮事件。</p></td>
</tr>
<tr class="even">
<td><p><strong>PropertyPages</strong></p></td>
<td><p>仅适用于 Windows 98 和 Windows 2000</p>
<p>标识为静态图像设备创建自定义属性页的 DLL 的名称和入口点。</p>
<p>有关 <strong>PropertyPages</strong> 条目的详细信息，请参阅 <a href="inf-files-for-still-image-devices.md" data-raw-source="[INF Files for Still Image Devices](inf-files-for-still-image-devices.md)">适用于静止图像设备的 INF 文件</a>。</p></td>
<td><p>可选</p>
<p>此项仅供 STI 驱动程序使用，并且对于 WIA 驱动程序已过时。</p>
<p>有关与 WIA 驱动程序开发人员相关的属性页的信息，请参阅此表后面的 PropertyPages 上的 <strong>说明</strong> 。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceData</strong></p></td>
<td><p>标识供应商提供的数据部分，其中包含要存储在注册表中的信息，在 <strong>DeviceData</strong> 项下。 对于 TWAIN 支持的设备，data 部分必须包含 TwainDS 条目 (请参阅 <a href="registry-entries-for-wia-drivers.md" data-raw-source="[Registry Entries for WIA Drivers](registry-entries-for-wia-drivers.md)">WIA 驱动程序) 的注册表项</a> 。</p></td>
<td><p>可选</p></td>
</tr>
<tr class="even">
<td><p><strong>事件</strong></p></td>
<td><p>标识供应商提供的数据部分，其中列出了仍为图像设备事件。 本节中的每个条目都必须采用以下格式：</p>
<p><em>事件名称</em><strong>= "</strong><em>String</em><strong>"、{</strong><em>GUID</em><strong>}、</strong>应用</p>
<p><em>事件名称是事件</em> 的内部名称， <em>String</em> 是事件的显示字符串， <em>guid</em> 是事件的 guid，而 <em>应用</em> 指定发生事件时要启动的图像处理应用程序。 若要启动当前注册的应用程序，请使用星号 (<strong>*</strong> <em>应用</em>) 。</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p><strong>PortSelect</strong></p></td>
<td><p>如果设备安装不需要端口选择页，则值为 "否" 会导致跳过此页。 此值还会导致<strong>CreateFileName</strong>条目值 (请参阅此表后面的<strong>CreateFileName</strong>和<strong>PortSelect</strong>上的<strong>说明</strong>) 自动设置为 "自动"。</p>
<p>如果值为 Message1，则会显示系统提供的消息，并将 <strong>CreateFileName</strong> 项值设置为 AUTO。</p>
<p>适用于需要手动安装的扫描仪和照相机。</p></td>
<td><p>可选</p>
<p>请注意，对于即插即用设备，将忽略 <strong>PortSelect</strong> ，但设备仍必须将 <strong>CreateFileName</strong> 条目值设置为 "自动"，以便 WIA 加载设备。 使用 <a href="/windows-hardware/drivers/install/inf-addreg-directive" data-raw-source="[&lt;strong&gt;INF AddReg Directive&lt;/strong&gt;](../install/inf-addreg-directive.md)"><strong>Inf AddReg 指令</strong></a> 将此条目添加到设备 inf 文件的 <a href="/windows-hardware/drivers/install/inf-ddinstall-section" data-raw-source="[&lt;strong&gt;INF DDInstall Section&lt;/strong&gt;](../install/inf-ddinstall-section.md)"><strong>inf DDInstall 部分</strong></a> 。</p></td>
</tr>
</tbody>
</table>

 

**注意**   为了与设备进行通信，用户模式客户端 (微型驱动程序) 必须向 WIA 服务询问设备的文件名以及指定要创建或打开的对象的名称的字符串。  (文件名不必是磁盘文件的名称。 ) 响应此类查询，WIA 服务将从 **CreateFileName** 注册表项中获取设备的文件名。  (*usbscan.sys* 和 *scsiscan.sys* 内核模式驱动程序会创建此项，这与类安装程序一样。 ) 微型驱动程序通过调用 [**IStiDeviceControl：： GetMyDevicePortName**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname) 方法接收此文件名。 然后，微型驱动程序可以在调用 Microsoft Windows SDK 文档) 中描述的 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea) (函数时使用此文件名，以打开设备的句柄。
如果手动安装了设备，则类安装程序会创建 **CreateFileName** 条目，并将其值设置为依赖于端口选择页面上用户选择的值： COM*X*、LPT*X*或 AUTO。 某些设备 (网络扫描仪，例如手动安装) ，无需端口。 在这种情况下，生成的端口选择对话框会使用户感到困惑。 可以通过在设备 INF 文件的 " [**Inf DDInstall" 部分**](../install/inf-ddinstall-section.md) 添加以下条目来阻止显示此对话框：

 

```INF
     PortSelect=NO
```

**注意**   此项值的副作用是**CreateFileName**项设置为 AUTO。 请注意，如果微型驱动程序接收到了文件名的自动，则它必须能够确定应该与之通信的设备。

**注意**   对于 PropertyPages，WIA 驱动程序必须使用不同的扩展性机制才能添加属性页。 它还必须将其自己的 GUID 添加到其 INF 文件中的 **UI 类 ID** 条目，并且必须提供特定的 UI 扩展性注册 (请参阅 [用户界面扩展注册表项](user-interface-extension-registry-entries.md)) 用于要替换的 ui 组件（如公用对话框）或添加（如上下文菜单和属性页）。 WIA 驱动程序还必须为组件本身提供 UI 扩展性注册。

 

 

### <a name="additional-inf-file-entries"></a>其他 INF 文件条目

下表中的条目必须位于设备 [**INF AddReg 指令**](../install/inf-addreg-directive.md)指向的部分中：

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
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>HardwareConfig</strong></p></td>
<td><p>指示设备使用的连接类型。</p>
<p>1，1−通用 WDM 设备</p>
<p>1，2− SCSI 设备</p>
<p>1，4− USB 设备</p>
<p>1、8−串行设备</p>
<p>1，16−并行设备</p></td>
<td><p>可选</p></td>
</tr>
<tr class="even">
<td><p><strong>USDClass</strong></p></td>
<td><p>指示微型驱动程序的 GUID。</p></td>
<td><p>可选。</p>
<p><strong>USDClass</strong>和<strong>CLSID</strong>条目中的 guid 必须与在微型驱动程序的<strong>DLLGETCLASSOBJECT</strong>函数中使用的 guid 匹配。 如果要编写 microdriver，则值应为 BB6CF8E2-1511-40bd-91BA-80D43C53064E。 否则，你必须使用 <em>genguid.exe</em>生成新的 GUID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CLSID</strong></p></td>
<td><p>指示微型驱动程序的 GUID。</p></td>
<td><p>可选。</p>
<p>请参阅前面的 <strong>USDClass</strong> 条目注释。</p></td>
</tr>
</tbody>
</table>

 

静止映像设备的默认类安装程序支持标准 [**INF CopyFiles 指令**](../install/inf-copyfiles-directive.md)。

静态映像设备（ *sti*）的默认 INF 文件为每种设备类型定义了两个安装节，如下所示：

-   [**INF DDInstall 部分**](../install/inf-ddinstall-section.md)，必须在供应商提供的 INF 文件的*DDInstall*部分中引用，如下表所示。

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
    <td><p>Include = sti</p></td>
    <td><p>需求 = STI。SBP2Section</p></td>
    </tr>
    <tr class="even">
    <td><p>USB</p></td>
    <td><p>Include = sti</p></td>
    <td><p>需求 = STI。USBSection</p></td>
    </tr>
    <tr class="odd">
    <td><p>SCSI</p></td>
    <td><p>Include = sti</p></td>
    <td><p>需求 = STI。SCSISection</p></td>
    </tr>
    <tr class="even">
    <td><p>串行</p></td>
    <td><p>Include = sti</p></td>
    <td><p>需求 = STI。SerialSection</p></td>
    </tr>
    </tbody>
    </table>

     

<!-- -->

-   INF DDInstall Services 部分，必须在供应商提供的 INF 文件的 [**Inf DDInstall 部分**](../install/inf-ddinstall-services-section.md) 中引用，如下表所示。

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
    <td><p>Include = sti</p></td>
    <td><p>需求 = STI。SBP2Section</p></td>
    </tr>
    <tr class="even">
    <td><p>USB</p></td>
    <td><p>Include = sti</p></td>
    <td><p>需求 = STI。USBSection</p></td>
    </tr>
    <tr class="odd">
    <td><p>SCSI</p></td>
    <td><p>Include = sti</p></td>
    <td><p>需求 = STI。SCSISection</p></td>
    </tr>
    <tr class="even">
    <td><p>串行</p></td>
    <td><p>Include = sti</p></td>
    <td><p>需求 = STI。SerialSection</p></td>
    </tr>
    </tbody>
    </table>

     

有关为静止图像设备创建 INF 文件的其他指南，你可以查看随 Windows 提供的、包含子类 "StillImage" 的任何 INF 文件。

若要将设备指定为 WIA 设备，微型驱动程序 INF 文件必须包含位于供应商提供的 INF 文件的 *DeviceData* 部分中的以下值。

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
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Server</strong></p></td>
<td><p>Local</p></td>
<td><p>将设备指定为本地设备。 这是可选的，如果供应商未指定输入值，则假定设备为本地设备。 也就是说，WIA_DIP_SERVER_NAME 属性设置为 Local。</p></td>
</tr>
<tr class="even">
<td><p><strong>MicroDriver</strong></p></td>
<td><p>供应商提供的 <em>.dll</em> 文件名</p></td>
<td><p>应将此项设置为供应商提供的用于实现 WIA microdriver 的 DLL 的名称。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UI DLL</strong></p></td>
<td><p>供应商提供的 <em>.dll</em> 文件名</p></td>
<td><p>过时且从未使用过。 以前，此条目指示供应商提供的用户界面 DLL 文件的名称。</p></td>
</tr>
<tr class="even">
<td><p><strong>UI 类 ID</strong></p></td>
<td><p>供应商提供的设备类标识符</p></td>
<td><p>指示供应商提供的用户界面支持的设备类。 这是可选的，如果供应商未指定输入值，WIA 会将 WIA_DIP_UI_CLSID 属性设置为 GUID_NULL 并使用默认的 WIA UI。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ICMProfiles</strong></p></td>
<td><p>供应商提供的颜色配置文件值</p></td>
<td><p>指定要置于 WIA_IPA_ICM_PROFILE_NAME 属性中的值。 如果未指定任何值，则使用标准 sRGB 配置文件 <em>Srgb 颜色空间配置文件。 icm</em> 。</p></td>
</tr>
</tbody>
</table>

 

仅当供应商提供 WIA MicroDriver 时，才需要 **MicroDriver** 项。

仅当供应商为图像设备提供自定义用户界面时，才需要用户界面) 条目 (UI。

**备注**

在为扫描仪开发 INF 文件时，可以使用 [MICROSOFT OS 描述符](/previous-versions/gg463179(v=msdn.10)) 来启用兼容 ID 功能。 当你执行此操作时，你允许一个扫描仪驱动程序与多个扫描仪模型兼容。

