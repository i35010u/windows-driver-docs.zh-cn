---
Description: 示例驱动程序安装程序信息 (.inf) 文件
title: 示例驱动程序安装程序信息 (.inf) 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b24563cf737fa71dc3594efb68d8aa0f9825263a
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464083"
---
# <a name="the-sample-driver-setup-information-inf-file"></a>示例驱动程序安装程序信息 (.inf) 文件


WpdHelloWorldDriver 项目包含名为的安装程序信息 (.inf) 文件*WpdHelloWorldDriver.inf*。 此文件包含 UMDF 参数和所需的 WUDF 共同安装程序的指令。 但是，此文件还包含参数和专用于 WPD 的指令。 下表列出了这些特定于 WPD 的参数、 指令和部分。

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
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Basic_Install.CoInstaller_AddReg</td>
<td align="left"></td>
<td align="left">本部分是必需的。
<ul>
<li><em>WudfCoInstaller.dll</em>必须列为共同安装程序。</li>
<li>Reg 根必须是"HKR"。</li>
<li>类型必须为 0x10000。</li>
<li>注册表指令必须存在。</li>
</ul>
<p>示例： <code>[Basic_Install.CoInstallers_AddReg]</code></p>
<p><code>HKR,,CoInstallers32,0x00010000,"WUDFCoInstaller.dll"</code></p></td>
</tr>
 <tr class="even">
<td align="left">Basic_Install.wdf</td>
<td align="left">UmdfService 指令</td>
<td align="left">此指令是必需的。
<ul>
<li>此指令的形式："UmdfService = ServiceName，ServiceInstallSection"。</li>
<li>引用部分 ("ServiceInstallSection") 必须存在。</li>
<li>指定的服务名称 ("ServiceName") 必须使用由 UmdfServiceOrder 指令。</li>
</ul>
<p>示例： <code>[Basic_Install.Wdf]</code></p>
<p><code>UmdfService=WpdHelloWorldDriver, WpdHelloWorldDriver_Install</code></p>
<p><code>UmdfServiceOrder=WpdHelloWorldDriver</code></p></td>
</tr>
<tr class="odd">
<td align="left">DDInstall.Services</td>
<td align="left">包括指令</td>
<td align="left">如果该驱动程序重用 MTP 类驱动程序组件，则需要此指令。 否则，它不应出现。
<p>必需的系统文件必须使用相应包括引用，或需要指令。 (这些文件是<em>WpdMtpDr.dll</em>， <em>WpdMtp.dll</em>， <em>WpdMtpUs.dll</em>， <em>WpdConns.dll</em> （适用于 Windows Vista 中)，并且任一<em>WpdUsb.sys</em> （对于 Windows Vista) 或<em>WinUsb.sys</em> （适用于 Windows 7 和更高版本）)。 此外必须引用的必要服务文件。 (需要引用的单个服务文件是<em>WpdUsb.sys</em> （适用于 Windows Vista) 或<em>WinUSB.sys</em> （适用于 Windows 7 和更高版本）。)</p></td>
</tr>
<tr class="even">
<td align="left">DDInstall.Services</td>
<td align="left">需要指令</td>
<td align="left">如果该驱动程序重用 MTP 类驱动程序组件，则需要此指令。 否则，它不应出现。
<p>必需的系统文件必须使用相应包括引用，或需要指令。 (这些文件是：<em>WpdMtpDr.dll</em>， <em>WpdMtp.dll,WpdMtpUs.dll</em>， <em>WpdConns.dll</em> （对于 Windows Vista)，并将<em>WpdUsb.sys</em> （适用于 Windows Vista) 或<em>WinUsb.sys</em> （适用于 Windows 7 和更高版本）)。 此外必须引用的必要服务文件。 (需要引用的单个服务文件是<em>WpdUsb.sys</em> （适用于 Windows Vista) 或<em>WinUSB.sys</em> （适用于 Windows 7 和更高版本）。)</p></td>
</tr>
<tr class="odd">
<td align="left">Device_AddReg</td>
<td align="left">EnableDefaultAutoPlaySupport directive</td>
<td align="left">此指令是必需的。
<ul>
<li>Reg 根必须是"HKR"。</li>
<li>类型必须为 0x10001。</li>
<li>必须设置有效的值 （0 或 1）。</li>
</ul>
<p>例如：</p>
<p><code>[Device_AddReg]</code></p>
<p><code>HKR,,"EnableDefaultAutoPlaySupport",0x10001,1</code></p></td>
</tr>
<tr class="even">
<td align="left">Device_AddReg</td>
<td align="left">EnableLegacySupport 指令</td>
<td align="left">此指令是必需的。
<ul>
<li>Reg 根必须是"HKR"。</li>
<li>类型必须为 0x10001。</li>
<li>必须设置有效的值 （0、 1、 2 或 3）。</li>
</ul>
<p>例如：</p>
<p><code>[Device_AddReg]</code></p>
<p><code>HKR,,"EnableLegacySupport",0x10001,1</code></p></td>
</tr>
<tr class="odd">
<td align="left">Device_AddReg</td>
<td align="left">UseWiaAutoPlay 指令</td>
<td align="left">此指令是可选的。
<ul>
<li>Reg 根必须是"HKR"。</li>
<li>类型必须为 0x10001。</li>
<li>必须设置有效的值 （0 或 1）。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left">安装</td>
<td align="left">UmdfLibraryVersion 指令</td>
<td align="left">此指令是必需的。
<p>此指令必须采用以下形式： n.n.n</p>
<p>示例： <code>[WpdHelloWorldDriver_Install]</code></p>
<p><code>UmdfLibraryVersion=1.0.0</code></p></td>
</tr>
<tr class="odd">
<td align="left">ServiceInstall</td>
<td align="left">ErrorControl 指令</td>
<td align="left">此指令是必需的。
<p>此指令必须指定的值为 1。</p>
<p>示例： <code>[WUDFRD_ServiceInstall]</code></p>
<p><code>ErrorControl=1</code></p></td>
</tr>
<tr class="even">
<td align="left">ServiceInstall</td>
<td align="left">ServiceType 指令</td>
<td align="left">此指令是必需的。
<p>此指令必须指定的值为 1。</p>
<p>例如：</p>
<p><code>[WUDFRD_ServiceInstall]</code></p>
<p><code>ServiceType=1</code></p></td>
</tr>
<tr class="odd">
<td align="left">ServiceInstall</td>
<td align="left">StartType 指令</td>
<td align="left">此指令是必需的。
<p>此指令必须指定的值为 3。</p>
<p>例如：</p>
<p><code>[WUDFRD_ServiceInstall]</code></p>
<p><code>StartType=3</code></p></td>
</tr>
<tr class="even">
<td align="left">版本</td>
<td align="left">类参数</td>
<td align="left">此参数是必需的。 必须设置为"WPD"。
<p>例如：</p>
<pre space="preserve"><code>[Version]
Class=WPD</code></pre></td>
</tr>
<tr class="odd">
<td align="left">版本</td>
<td align="left">ClassGuid 参数</td>
<td align="left">此参数是必需的。 必须设置为有效的 GUID。
<p>例如：</p>
<pre space="preserve"><code>[Version]
ClassGuid={EEC5AD98-8080-425f-922A-DABF3DE3F69A}</code></pre></td>
</tr>
<tr class="even">
<td align="left">WpdHelloWorldDriver_Install</td>
<td align="left">DriverCLSID 指令</td>
<td align="left">此指令是必需的。
<p>此指令必须指定一个格式正确的 GUID。</p>
<p>例如：</p>
<pre space="preserve"><code>[WpdHelloWorldDriver_Install]
DriverCLSID="{EC7445EE-BC00-4CED-AFE7-A52849F10239}"</code></pre></td>
</tr>
<tr class="odd">
<td align="left">WpdHelloWorldDriver_Install</td>
<td align="left">ServiceBinary 指令</td>
<td align="left">此指令是必需的。
<p>此指令必须指定窗体的路径:"%12%\wudfrd.sys"</p>
<p>例如：</p>
<p><code>[WUDFRD_ServiceInstall]</code></p>
<p><code>ServiceBinary=%12%\WUDFRd.sys</code></p></td>
</tr>
</tbody>
</table>

 

 

 




