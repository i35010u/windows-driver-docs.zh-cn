---
description: 示例驱动程序安装程序信息 (.inf) 文件
title: 示例驱动程序安装程序信息 (.inf) 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 259a084e62ff19606f130881f5c7fdbc7715ceed
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969456"
---
# <a name="the-sample-driver-setup-information-inf-file"></a>示例驱动程序安装程序信息 (.inf) 文件


WpdHelloWorldDriver 项目包含 ( 名为 *WpdHelloWorldDriver*的) 文件的安装信息。 此文件包含 WUDF 共同安装程序所需的 UMDF 参数和指令。 但是，此文件还包含 WPD 专用的参数和指令。 下表列出了这些特定于 WPD 的参数、指令和节。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">部分</th>
<th align="left">指令或参数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Basic_Install. CoInstaller_AddReg</td>
<td align="left"></td>
<td align="left">本部分是必需的。
<ul>
<li><em>WudfCoInstaller.dll</em> 必须作为共同安装程序列出。</li>
<li>注册表根必须是 "HKR"。</li>
<li>类型必须为0x10000。</li>
<li>注册表指令必须存在。</li>
</ul>
<p>示例：<code>[Basic_Install.CoInstallers_AddReg]</code></p>
<p><code>HKR,,CoInstallers32,0x00010000,"WUDFCoInstaller.dll"</code></p></td>
</tr>
 <tr class="even">
<td align="left">Basic_Install wdf</td>
<td align="left">UmdfService 指令</td>
<td align="left">此指令是必需的。
<ul>
<li>此指令的形式为： "UmdfService = ServiceName，ServiceInstallSection"。</li>
<li>引用的节 ( "ServiceInstallSection" ) 必须存在。</li>
<li>指定的服务名称 ( "ServiceName" ) 必须由 UmdfServiceOrder 指令使用。</li>
</ul>
<p>示例：<code>[Basic_Install.Wdf]</code></p>
<p><code>UmdfService=WpdHelloWorldDriver, WpdHelloWorldDriver_Install</code></p>
<p><code>UmdfServiceOrder=WpdHelloWorldDriver</code></p></td>
</tr>
<tr class="odd">
<td align="left">DDInstall</td>
<td align="left">包含指令</td>
<td align="left">如果驱动程序重用 MTP 类驱动程序组件，则需要此指令。 否则，不应出现此情况。
<p>必须使用适当的包含或需要指令来引用所需的系统文件。  (<em>WpdMtpDr.dll</em>、 <em>WpdMtp.dll</em>、 <em>WpdMtpUs.dll</em>、 <em>WpdConns.dll</em> (用于 windows vista) ，以及 windows Vista <em>WpdUsb.sys(或 </em> <em>)WinUsb.sys(</em> # A7。 还必须引用必要的服务文件。  (需要引用的单个服务文件 (<em>WpdUsb.sys</em> 适用于 windows Vista) 或 <em>WinUSB.sys</em> (windows 7 和更高版本) 。 ) </p></td>
</tr>
<tr class="even">
<td align="left">DDInstall</td>
<td align="left">需要指令</td>
<td align="left">如果驱动程序重用 MTP 类驱动程序组件，则需要此指令。 否则，不应出现此情况。
<p>必须使用适当的包含或需要指令来引用所需的系统文件。  (这些文件是： <em>WpdMtpDr.dll</em>、 <em>WpdMtp.dll、WpdMtpUs.dll</em>、 <em>WpdConns.dll</em> (用于 windows Vista) ，并 <em>WpdUsb.sys</em> Windows vista <em> (或)WinUsb.sys(</em> # A7。 还必须引用必要的服务文件。  (需要引用的单个服务文件 (<em>WpdUsb.sys</em> 适用于 windows Vista) 或 <em>WinUSB.sys</em> (windows 7 和更高版本) 。 ) </p></td>
</tr>
<tr class="odd">
<td align="left">Device_AddReg</td>
<td align="left">EnableDefaultAutoPlaySupport 指令</td>
<td align="left">此指令是必需的。
<ul>
<li>注册表根必须是 "HKR"。</li>
<li>类型必须为0x10001。</li>
<li>必须设置 (0 或 1) 有效的值。</li>
</ul>
<p>示例：</p>
<p><code>[Device_AddReg]</code></p>
<p><code>HKR,,"EnableDefaultAutoPlaySupport",0x10001,1</code></p></td>
</tr>
<tr class="even">
<td align="left">Device_AddReg</td>
<td align="left">EnableLegacySupport 指令</td>
<td align="left">此指令是必需的。
<ul>
<li>注册表根必须是 "HKR"。</li>
<li>类型必须为0x10001。</li>
<li>必须设置有效的 (0、1、2或 3) 的值。</li>
</ul>
<p>示例：</p>
<p><code>[Device_AddReg]</code></p>
<p><code>HKR,,"EnableLegacySupport",0x10001,1</code></p></td>
</tr>
<tr class="odd">
<td align="left">Device_AddReg</td>
<td align="left">UseWiaAutoPlay 指令</td>
<td align="left">此指令是可选的。
<ul>
<li>注册表根必须是 "HKR"。</li>
<li>类型必须为0x10001。</li>
<li>必须设置 (0 或 1) 有效的值。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left">安装</td>
<td align="left">UmdfLibraryVersion 指令</td>
<td align="left">此指令是必需的。
<p>此指令的格式必须为： n。 n</p>
<p>示例：<code>[WpdHelloWorldDriver_Install]</code></p>
<p><code>UmdfLibraryVersion=1.0.0</code></p></td>
</tr>
<tr class="odd">
<td align="left">ServiceInstall</td>
<td align="left">ErrorControl 指令</td>
<td align="left">此指令是必需的。
<p>此指令必须将值指定为1。</p>
<p>示例：<code>[WUDFRD_ServiceInstall]</code></p>
<p><code>ErrorControl=1</code></p></td>
</tr>
<tr class="even">
<td align="left">ServiceInstall</td>
<td align="left">ServiceType 指令</td>
<td align="left">此指令是必需的。
<p>此指令必须将值指定为1。</p>
<p>示例：</p>
<p><code>[WUDFRD_ServiceInstall]</code></p>
<p><code>ServiceType=1</code></p></td>
</tr>
<tr class="odd">
<td align="left">ServiceInstall</td>
<td align="left">StartType 指令</td>
<td align="left">此指令是必需的。
<p>此指令必须将值指定为3。</p>
<p>示例：</p>
<p><code>[WUDFRD_ServiceInstall]</code></p>
<p><code>StartType=3</code></p></td>
</tr>
<tr class="even">
<td align="left">Version</td>
<td align="left">类参数</td>
<td align="left">此参数是必需的。 必须设置为 "WPD"。
<p>示例：</p>
<pre space="preserve"><code>[Version]
Class=WPD</code></pre></td>
</tr>
<tr class="odd">
<td align="left">Version</td>
<td align="left">ClassGuid 参数</td>
<td align="left">此参数是必需的。 必须设置为有效的 GUID。
<p>示例：</p>
<pre space="preserve"><code>[Version]
ClassGuid={EEC5AD98-8080-425f-922A-DABF3DE3F69A}</code></pre></td>
</tr>
<tr class="even">
<td align="left">WpdHelloWorldDriver_Install</td>
<td align="left">DriverCLSID 指令</td>
<td align="left">此指令是必需的。
<p>此指令必须指定一个格式正确的 GUID。</p>
<p>示例：</p>
<pre space="preserve"><code>[WpdHelloWorldDriver_Install]
DriverCLSID="{EC7445EE-BC00-4CED-AFE7-A52849F10239}"</code></pre></td>
</tr>
<tr class="odd">
<td align="left">WpdHelloWorldDriver_Install</td>
<td align="left">ServiceBinary 指令</td>
<td align="left">此指令是必需的。
<p>此指令必须指定以下格式的路径： "%12% \wudfrd.sys"</p>
<p>示例：</p>
<p><code>[WUDFRD_ServiceInstall]</code></p>
<p><code>ServiceBinary=%12%\WUDFRd.sys</code></p></td>
</tr>
</tbody>
</table>

 

 

 




