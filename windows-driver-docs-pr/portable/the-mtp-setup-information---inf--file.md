---
Description: MTP 安装程序信息 (.inf) 文件
title: MTP 安装程序信息 (.inf) 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f76f42c17479d35ea63ae846708bbf3900f3d6f6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349327"
---
# <a name="the-mtp-setup-information-inf-file"></a>MTP 安装程序信息 (.inf) 文件


Microsoft 提供了一组类驱动程序以支持媒体传输协议 (MTP)。 如果设备支持 MTP，可以使用这些驱动因素之一。 除了类驱动程序，Microsoft 提供要安装类驱动程序的安装程序信息 (.inf) 文件。 此文件命名为*WpdMtp.inf*。

如果你的 MTP 设备具有独特的要求，创建一个新的安装信息 (.inf) 文件所基于的原始版本*WpdMtp.inf*。 (您不能修改*WpdMtp.inf*直接。)

下表描述了中找到的特定需求指令*WpdMtp.inf*和可能可以对由给定的指令标识的部分进行的修改。

下表中的条目可以支持任何三个传输 （USB、 IP 或蓝牙）。 请注意，每个传输协议需要唯一的安装部分。 此外请注意，在 Windows 7 中仅支持蓝牙传输。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">需要指令</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">需要 = WPD。MTP，WINUSB。NT</td>
<td align="left">WPD。MTP 部分标识可复制并注册的驱动程序文件。 以下内容适用于 Windows Vista 和 Windows Media Player 11。
<pre space="preserve"><code>;;[DDInstall]
;;Include = wpdmtp.inf
;;Needs = WPD.MTP</code></pre>
<p>从 Windows 7 开始<em>WinUsb.sys</em>替换<em>WpdUsb.sys</em>作为的 MTP 设备通过 USB 连接到计算机的较低的筛选器驱动程序。 以下指令时要求供应商的 INF 用以<em>WinUsb.inf</em>和特定 WinUSB 部分：</p>
<pre space="preserve"><code>;;[DDInstall]
;;Include = wpdmtp.inf, WINUSB.INF
;;Needs = WPD.MTP, WINUSB.NT</code></pre></td>
</tr>
<tr class="even">
<td align="left">需要 = WPD。MTP。注册</td>
<td align="left">WPD。MTP。注册部分来实现四个任务：
<ol>
<li>注册内核模式驱动程序 (包括<em>WPDUSB.sys</em>作为低筛选器驱动程序如果要在 Windows Vista 或 Windows XP 上安装该设备)。</li>
<li>启用默认 MTP 自动播放支持。</li>
<li>启用旧版应用程序兼容性支持 （默认值 0xFFFFFFFF 允许 WPD 类安装程序来查询设备的功能）。</li>
<li>设置传输驱动程序的类标识符。</li>
</ol>
<pre space="preserve"><code>;;[DDInstall.hw]
;;Include = wpdmtp.inf
;;Needs = WPD.MTP.Registration</code></pre></td>
</tr>
<tr class="odd">
<td align="left">Needs = WPD.MTP.Registration.Basic</td>
<td align="left">WPD。MTP。Registration.Basic 部分，可以自定义任务 2 和 3 中前面的列表。 例如，可以设置应用程序兼容性，以支持 Windows 图像采集 (WIA) 使用的值 0x01 或 Windows 媒体设备管理器 (WMDM) 使用 0x02 的值。
<pre space="preserve"><code>;;[DDInstall.hw]
;;Include = wpdmtp.inf
;;Needs = WPD.MTP.Registration.Basic</code></pre></td>
</tr>
<tr class="even">
<td align="left">Needs = WPD.MTP.Services</td>
<td align="left">WPD。MTP。服务部分中添加驱动程序服务 （和默认服务参数）。 这包括 WUDF 并<em>WPDUSB.sys</em> （适用于 Windows Vista 和仅适用于 Windows XP）。
<pre space="preserve"><code>;;[DDInstall.Services]
;;Include = wpdmtp.inf
;;Needs = WPD.MTP.Services</code></pre></td>
</tr>
<tr class="odd">
<td align="left">需要 = WPD。MTP。共同安装程序</td>
<td align="left">WPD。MTP。共同安装程序部分标识共同安装程序。 （若要安装的 MTP 设备，Windows 用户模式驱动程序框架 (UMDF) 共同安装程序使用。）
<p>本部分是必需的 Windows 7、 Windows Vista 和 Windows Media Player 11。 （它不是必需的 MTP 驱动程序支持 Windows Media Player 10。）</p>
<pre space="preserve"><code>;;[DDInstall.CoInstallers]
;;Include = wpdmtp.inf
;;Needs = WPD.MTP.CoInstallers</code></pre></td>
</tr>
<tr class="even">
<td align="left">Needs = WPD.MTP.Wdf</td>
<td align="left">WPD.MTP.Wdf 部分标识 Windows 用户模式驱动程序框架 (UMDF) 服务和其二进制文件 (<em>WPDMTPDR.dll</em>)。
<p>本部分是必需的 Windows 7、 Windows Vista 和 Windows Media Player 11。 （它不是必需的 MTP 驱动程序支持 Windows Media Player 10。）</p>
<pre space="preserve"><code>;;[DDInstall.CoInstallers]
;;Include = wpdmtp.inf
;;Needs = WPD.MTP.Wdf</code></pre></td>
</tr>
</tbody>
</table>

 

 

 




