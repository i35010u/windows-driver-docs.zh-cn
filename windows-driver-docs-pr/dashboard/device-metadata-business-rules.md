---
title: 设备元数据业务规则
description: 设备元数据业务规则
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcb461a629c50a9364ac9ae1c7c2cbcfeee7c306
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800381"
---
# <a name="device-metadata-business-rules"></a>设备元数据业务规则

通过仪表板提交设备元数据包时，你应该确保：

- 为正确的设备下载包。

- 通过关联硬件 ID 和型号 ID 明确标识正确的包，并且不存在冲突。

- 不会将预览包下载为发行的包。

## <a name="general-rules-for-submitting-device-metadata"></a>提交设备元数据的一般规则

通过仪表板提交包时，适用以下一般规则。

- 所有包都必须不含恶意软件。
- 每个设备元数据包都必须用公司的 Microsoft Authenticode 证书进行签名。
- 你的公司创建的每个体验的名称在你的公司中都必须唯一。
- 包的友好名称在包含该包的体验中必须唯一。
- 包的原始文件名必须唯一。
- 所有包中的所有硬件 ID 都必须唯一。 硬件 ID 不能匹配你的公司或另一个公司创建的另一个体验中的硬件 ID。
- 所有包中的所有型号 ID 都必须唯一。 型号 ID 不能匹配你的公司或另一个公司创建的另一个体验中的型号 ID。
- 指向设备的任何有效徽标提交的链接都必须包含在设备元数据提交中。 每个有效的徽标提交必须包括列在设备元数据提交中的主要设备类型。
- 要更新现有体验中的包，你必须首先删除现有的包，创建一个新包，然后将新包上载到现有体验。
- 一个包所包含的 ID 不得超过 1,000 个。 其中包括硬件 ID 和型号 ID。

### <a name="device-metadata-types"></a>设备元数据类型

不同类型的设备元数据包必须遵守不同的规则。 另外，Device Stage 元数据中的不同设备类别必须遵守特定规则。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>元数据类型</th>
<th>适用于</th>
<th>要求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>设备和打印机文件夹</p></td>
<td><ul>
<li><p>所有设备</p></li>
<li><p>包含 UWP 设备应用的设备</p></li>
<li><p>包含特权应用的设备</p></li>
</ul></td>
<td><p>设备必须仅使用没有关联 Windows® 徽标提交的内置驱动程序，或者具有绑定到设备体验的自定义驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>Device Stage</p></td>
<td><ul>
<li><p>数码相机</p>
<ul>
<li><p>Imaging.Camera</p></li>
</ul></li>
<li><p>便携式媒体播放机</p>
<p>Multimedia.PMP</p></li>
<li><p>移动电话</p>
<ul>
<li><p>Communication.Phone.Cell</p></li>
</ul></li>
<li><p>打印机、传真机和扫描仪</p>
<ul>
<li><p>PrintFax</p></li>
<li><p>PrintFax.Fax</p></li>
<li><p>PrintFax.MFP</p></li>
<li><p>PrintFax.Printer</p></li>
<li><p>PrintFax.Printer.Inkjet</p></li>
<li><p>PrintFax.Printer.Laser</p></li>
<li><p>PrintFax.Printer.3D</p></li>
<li><p>Imaging.Scanner</p></li>
</ul></li>
<li><p>计算机</p>
<ul>
<li><p>Computer.AllInOne</p></li>
<li><p>Computer.Desktop</p></li>
<li><p>Computer.Desktop.LowProfile</p></li>
<li><p>Computer.Desktop.Pizzabox</p></li>
<li><p>Computer.Laptop</p></li>
<li><p>Computer.Lunchbox</p></li>
<li><p>Computer.Netbook</p></li>
<li><p>Computer.Notebook</p></li>
<li><p>Computer.Notebook.Sub</p></li>
<li><p>Computer.Portable</p></li>
<li><p>Computer.Rackmount</p></li>
<li><p>Computer.Sealed</p></li>
<li><p>Computer.Server</p></li>
<li><p>Computer.SpaceSaving</p></li>
<li><p>Computer.Tablet</p></li>
<li><p>Computer.ThinClient</p></li>
<li><p>Computer.Tower</p></li>
<li><p>Computer.Tower.Mini</p></li>
</ul></li>
<li><p>键盘和鼠标</p>
<ul>
<li><p>Input.Keyboard</p></li>
<li><p>Input.Mouse</p></li>
<li><p>Input.Trackball</p></li>
</ul></li>
<li><p>智能卡</p>
<ul>
<li><p>PersonalIdentity.Smartcard</p></li>
<li><p>Media.Smartcard</p></li>
</ul></li>
<li><p>移动宽带设备</p>
<ul>
<li><p>Network.MobileBroadband</p></li>
</ul></li>
<li><p>摄像头</p>
<ul>
<li><p>Imaging.Webcam</p></li>
</ul></li>
<li><p>一般便携式设备</p>
<ul>
<li><p>Other.Portable</p></li>
</ul></li>
</ul></td>
<td><p>每个设备都必须有一个 Windows 徽标提交。</p></td>
</tr>
</tbody>
</table>

### <a name="experience-rules"></a>体验规则

- 单个体验中的所有设备元数据包都必须支持相同的硬件 ID 和型号 ID。

- 在某个体验中，当你将特定区域设置、预览状态和 Windows 操作系统合并在一个包时，该合并在体验的每个包中必须唯一。 例如，在你的体验中，对于区域设置 A，你可以针对每个 Windows 操作系统包括一个发行包和预览包。 同一个体验不能为区域设置 A 和该 Windows 操作系统包含任何其他发行包或预览包。

- 在一个体验中，你只能为每个 Windows 操作系统版本设置一个默认预览区域设置包和一个默认发行包。

### <a name="unique-device-stage-metadata-submissions"></a>唯一 Device Stage 元数据提交

要提交电脑元数据包，请参阅[提交电脑设备清单包](./index.yml)。

要提交移动宽带元数据包，请参阅[提交移动宽带设备清单包](submit-a-mobile-broadband-device-manifest-package.md)。

要提交多区域设置元数据包，请参阅[提交多区域设置设备清单包](submit-a-multiple-locale-device-manifest-package.md)。

### <a name="uwp-device-app-limits"></a>UWP 设备应用的限制

设备制造商在可以在设备元数据中指定用于自动安装和应用特权的 UWP 应用的数量方面受到限制。 例如，每个外围设备生产商 (IHV) 可以最多提交配置为自动安装的一个应用，以及最多一个指定为特权应用的应用。 IHV 可以提交满足这两个限制条件的一个应用，或者提交两个应用，每一个仅满足一个限制条件。

>[!IMPORTANT]
>设备生产商可以向 Microsoft Store 提交的 UWP 设备应用的总数没有限制；这些限制仅适用于单个设备元数据包。

移动运营商和 OEM 在他们可以在设备元数据中指定的应用数量方面有不同的限制。 有关详细信息，OEM 应联系其 Microsoft OEM 代表。

在每个设备元数据包中，适用下列限制：

|开发人员|自动安装应用限制|特权应用限制|
|----|----|----|
|IHV|1|1|
|移动运营商|1|8|
|OEM|联系 Microsoft|联系 Microsoft|

## <a name="related-topics"></a>相关主题

- [创建设备元数据体验](create-a-device-metadata-experience.md)

- [管理设备元数据体验](manage-device-metadata-experiences.md)

- [提交设备元数据包（仪表板帮助）](submit-a-device-metadata-package--dashboard-help-.md)
