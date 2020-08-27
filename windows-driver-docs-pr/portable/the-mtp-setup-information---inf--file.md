---
description: MTP 安装程序信息 (.inf) 文件
title: MTP 安装程序信息 (.inf) 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05f1c65d9c9c920d81bd597b68f56d2f1768c791
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969460"
---
# <a name="the-mtp-setup-information-inf-file"></a>MTP 安装程序信息 (.inf) 文件


Microsoft 提供一组类驱动程序来支持 (MTP) 的媒体传输协议。 如果设备支持 MTP，则可以使用其中一个驱动程序。 除了类驱动程序以外，Microsoft 还提供了安装信息 ( .inf) 文件来安装类驱动程序。 此文件名为 *WpdMtp*。

如果 MTP 设备有独特的要求，请在 *WpdMtp*的原始版本) 文件 ( 创建新的设置信息。  (无法直接修改 *WpdMtp* 。 ) 

下表介绍了 *WpdMtp* 中的特定需求指令以及可对由给定指令标识的部分进行的可能修改。

下表中的条目可支持任何三个传输 (USB、IP 或 Bluetooth) 。 请注意，每个传输都需要一个唯一的安装部分。 另外请注意，只有 Windows 7 支持蓝牙传输。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">需要指令</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">需求 = WPD。MTP，WINUSB。NT</td>
<td align="left">WPD。MTP 部分标识将复制和注册的驱动程序文件。 以下内容适用于 Windows Vista 和 Windows Media Player 11。
<pre space="preserve"><code>;;[DDInstall]
;;Include = wpdmtp.inf
;;Needs = WPD.MTP</code></pre>
<p>从 Windows 7 开始， <em>WinUsb.sys</em> 将 <em>WpdUsb.sys</em> 替换为使用 USB 连接到计算机的 MTP 设备的较低筛选器驱动程序。 要使供应商的 INF 包括 <em>WinUsb</em> 和特定 WinUsb 部分，需要以下指令：</p>
<pre space="preserve"><code>;;[DDInstall]
;;Include = wpdmtp.inf, WINUSB.INF
;;Needs = WPD.MTP, WINUSB.NT</code></pre></td>
</tr>
<tr class="even">
<td align="left">需求 = WPD。MTP.报名</td>
<td align="left">WPD。MTP.注册部分完成了四项任务：
<ol>
<li>如果要在 Windows Vista 或 Windows XP) 上安装设备，请将 (的内核模式驱动程序注册到包含较低筛选器驱动程序的 <em>WPDUSB.sys</em> 。</li>
<li>启用默认 MTP 自动播放支持。</li>
<li>启用旧版应用程序兼容性支持 (默认值0xFFFFFFFF 允许 WPD 类安装程序查询设备功能) 。</li>
<li>设置传输驱动程序的类标识符。</li>
</ol>
<pre space="preserve"><code>;;[DDInstall.hw]
;;Include = wpdmtp.inf
;;Needs = WPD.MTP.Registration</code></pre></td>
</tr>
<tr class="odd">
<td align="left">需求 = WPD。MTP.注册基本</td>
<td align="left">WPD。MTP."注册" 部分用于自定义上一列表中的任务2和3。 例如，你可以将应用程序兼容性设置为支持 Windows 图像获取 (WIA) ，方法是使用值0x01 或 Windows Media 设备管理器 (WMDM) ，使用值0x02。
<pre space="preserve"><code>;;[DDInstall.hw]
;;Include = wpdmtp.inf
;;Needs = WPD.MTP.Registration.Basic</code></pre></td>
</tr>
<tr class="even">
<td align="left">需求 = WPD。MTP.服务器</td>
<td align="left">WPD。MTP.服务部分添加了驱动程序服务 (和默认的服务参数) 。 这包括适用于 Windows Vista 和 Windows XP 的 WUDF 和 <em>WPDUSB.sys</em> () 。
<pre space="preserve"><code>;;[DDInstall.Services]
;;Include = wpdmtp.inf
;;Needs = WPD.MTP.Services</code></pre></td>
</tr>
<tr class="odd">
<td align="left">需求 = WPD。MTP.CoInstallers</td>
<td align="left">WPD。MTP.CoInstallers 部分标识共同安装程序。  (安装 MTP 设备，则使用 Windows 用户模式驱动程序框架 (UMDF) 共同安装程序。 ) 
<p>Windows 7、Windows Vista 和 Windows Media Player 11 需要此部分。  (支持 Windows Media Player 10 的 MTP 驱动程序不需要它。 ) </p>
<pre space="preserve"><code>;;[DDInstall.CoInstallers]
;;Include = wpdmtp.inf
;;Needs = WPD.MTP.CoInstallers</code></pre></td>
</tr>
<tr class="even">
<td align="left">需求 = WPD</td>
<td align="left">WPD 节标识 Windows 用户模式驱动程序框架 (UMDF) 服务及其二进制 (<em>WPDMTPDR.dll</em>) 。
<p>Windows 7、Windows Vista 和 Windows Media Player 11 需要此部分。  (支持 Windows Media Player 10 的 MTP 驱动程序不需要它。 ) </p>
<pre space="preserve"><code>;;[DDInstall.CoInstallers]
;;Include = wpdmtp.inf
;;Needs = WPD.MTP.Wdf</code></pre></td>
</tr>
</tbody>
</table>

 

 

 




