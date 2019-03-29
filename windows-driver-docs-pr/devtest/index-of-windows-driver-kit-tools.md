---
title: Windows 驱动程序工具包工具的索引
description: Windows 驱动程序工具包工具的索引
ms.assetid: 26db88c4-8fb8-4308-ab8a-1a1eef5e19d8
keywords:
- 禁用程序工具
- DbgCon 工具
- Sniffir 工具
- Sledge 工具
- 调用验证程序使用情况工具
- CUV 工具
- 列出工具 WDK，
- 驱动程序开发工具 WDK 列出
- 睡眠状态选择器
- 一个大爆冷门
- Acpislp
- 手动电源状态更改测试
- GUIDGen WDK
- GUID 生成器 WDK
- GUIDGen.exe WDK
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: cac00eb60b57dee3eb425bfa6ec86f8c25abd7c3
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349558"
---
# <a name="index-of-windows-driver-kit-tools"></a>Windows 驱动程序工具包工具的索引


本主题提供有关包含 Windows Driver Kit (WDK) 中的工具的基本信息。 本主题还包括对其他工具，可用于驱动程序开发的引用。 这些其他工具都是可用的操作系统或作为单独的下载可用的一部分。 有关每个工具的详细信息，请参阅本主题，其中介绍的工具中的文档。

有关如何获取最新的 WDK 的信息，请参阅[Windows Driver Kit (WDK)](https://go.microsoft.com/fwlink/p/?linkid=261797)。

本主题包括：

-   [WDK 工具的索引](#index-of-wdk-tools)
-   [什么是 Windows 8.1 的 WDK 中的新增功能](#what-s-new-in-the-wdk-for-windows8-1)
-   [什么是适用于 Windows 8 WDK 中的新增功能](#what-s-new-in-the-wdk-for-windows8)
-   [更改的内容在 WDK 中针对 Windows 8](#what-s-changed-in-the-wdk-for-windows8)
-   [支持的平台](#supported-platforms)

### <a name="index-of-wdk-tools"></a>WDK 工具的索引

下表中的信息描述可用于 Windows 驱动程序开发人员的工具。 工具列表包括 WDK 附带工具 (如所示**WDK 工具**字段)，还包括一些工具，是单独提供的或与 Windows 一起安装的。 下面列出了通常可用于所有驱动程序的工具[的所有驱动程序](#tech-all)。 特定于一种技术的工具组合在一起，例如，工具，是特定于[Windows 便携式设备 (WPD) 驱动程序](#tech-wpd)或[传感器](#tech-sensors)。

-   [音频/视频驱动程序](#tech-audio-video)
-   [蓝牙驱动程序](#tech-bluetooth)
-   [Windows 图像采集 (WIA) 驱动程序](#tech_wia)
-   [Windows 便携设备 (WPD) 驱动程序](#tech-wpd)
-   [打印机驱动程序](#tech-printer)
-   [传感器](#tech-sensors)
-   [所有驱动程序](#tech-all)

**请注意**  Visual Studio 环境变量，%windowssdkdir%，表示 Windows 工具包 WDK 的此版本的安装的目录，例如，c: 路径\\Program Files (x86)\\Windows 工具包\\8.1。

 

### 技术：音频 / 视频驱动程序 <a name="tech-audio-video"></a>

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">工具名称</th>
<th align="left">工具位置</th>
<th align="left">说明和帮助文件的位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>显示颜色校准工具 (Dccw.exe)</p>
<p><strong>WDK 工具：</strong>否</p></td>
<td align="left"><p>%Windir%\System32\Dccw.exe</p></td>
<td align="left"><p>校准工具，以便用户可以调整其显示颜色，使其更接近于 Windows、 World Wide Web 国际标准红-绿-蓝 (sRGB) 颜色空间。</p>
</tr>
<tr class="even">
<td align="left"><p>GraphEdt (Graphedt.exe)</p>
<p><strong>WDK 中的工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\graphedt.exe</p>
<p>%WindowsSdkDir%\tools\x64\graphedt.exe</p></td>
<td align="left"><p>生成的筛选器关系图来测试流音频/视频捕获驱动程序。</p>
<p>文档：</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=9230" data-raw-source="[Overview of GraphEdit](https://go.microsoft.com/fwlink/p/?linkid=9230)">GraphEdit 的概述</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSStudio (KsStudio.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\KsStudio.exe</p>
<p>%WindowsSdkDir%\tools\x64\KsStudio.exe</p>
<div class="alert">
<strong>请注意</strong>  必须由具有管理员权限的用户运行此工具。
</div>
<div>
 
</div></td>
<td align="left"><p>此工具可以构造的图形表示形式显示筛选器和筛选器的内部节点之间的 pin pin 连接的筛选器关系图。</p>
<p>%WindowsSdkDir%\tools\x86\KsStudio.chm</p>
<p>%WindowsSdkDir%\tools\x64\KsStudio.chm</p>
<p>请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff554257" data-raw-source="[AVStream Testing and Debugging](https://msdn.microsoft.com/library/windows/hardware/ff554257)">AVStream 测试和调试</a>有关详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>USB 设备查看器 (Usbview.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\Usbview.exe</p>
<p>%WindowsSdkDir%\tools\x64\Usbview.exe</p></td>
<td align="left"><p>枚举 USB 主控制器、 USB 集线器和附加的 USB 设备，并可以查询有关注册表中和通过 USB 请求到的设备的设备的信息。</p>
<p>源代码有关 USB 设备查看器可从代码库，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=256205" data-raw-source="[USBVIEW Sample Application](https://go.microsoft.com/fwlink/p/?linkid=256205)">USBVIEW 示例应用程序</a>。</p></td>
</tr>
</tbody>
</table>

 

### 技术：蓝牙驱动程序 <a name="tech-bluetooth"></a>

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">工具名称</th>
<th align="left">工具位置</th>
<th align="left">说明和帮助文件的位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>蓝牙查询记录验证程序 (Sdpverify.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\Sdpverifiy.exe</p>
<p>%WindowsSdkDir%\tools\x64\Sdpverifiy.exe</p></td>
<td align="left"><p>显示 Windows 将其解释蓝牙设备的查询记录。</p>
<p>WDK 文档：</p>
<p><a href="bluetooth-inquiry-record-verifier.md" data-raw-source="[Bluetooth Inquiry Record Verifier](bluetooth-inquiry-record-verifier.md)">蓝牙查询记录验证工具</a></p></td>
</tr>
</tbody>
</table>

 

### 技术：Windows 图像采集 (WIA) 驱动程序<a name="tech_wia"></a>

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">工具名称</th>
<th align="left">工具位置</th>
<th align="left">说明和帮助文件的位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WIADbgCfg (Wiadbgcfg.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\wiadbgcfg.exe</p>
<p>%WindowsSdkDir%\tools\x64\wiadbgcfg.exe</p></td>
<td align="left"><p>启用日志记录的 WIA 驱动程序 （Windows Server 2008 和更高版本的 Windows）。</p>
<div class="alert">
<strong>请注意</strong>  对于早期版本的 Windows，请使用 WIALogCfg。
</div>
<div>
 
</div>
<p>%WindowsSdkDir%\tools\x86\wiadbgcfg.htm</p>
<p>%WindowsSdkDir%\tools\x64\wiadbgcfg.htm</p></td>
</tr>
<tr class="even">
<td align="left"><p>WIAInfo2 (Wiainfo2.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\wiainfo2.exe</p>
<p>%WindowsSdkDir%\tools\x64\wiainfo2.exe</p></td>
<td align="left"><p>显示 WIA 项树，以便可以查看和编辑 WIA 的设备驱动程序属性。</p>
<p>%WindowsSdkDir%\tools\x86\wiainfo2.htm</p>
<p>%WindowsSdkDir%\tools\x64\wiainfo2.htm</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WIAPreview (Wiapreview.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\wiapreview.exe</p>
<p>%WindowsSdkDir%\tools\x86\wiapreview.exe</p></td>
<td align="left"><p>演示如何使用 WIA 预览组件和驱动程序的分段的筛选器。</p>
<p>%WindowsSdkDir%\tools\x64\wiapreview.htm</p>
<p>%WindowsSdkDir%\tools\x86\wiapreview.htm</p></td>
</tr>
<tr class="even">
<td align="left"><p>WIATest (Wiatest.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\wiatest.exe</p>
<p>%WindowsSdkDir%\tools\x86\wiatest.exe</p></td>
<td align="left"><p>显示创建的驱动程序，公开该驱动程序和每个属性的当前值的 Windows 图像采集 (WIA) 属性的项树。 此工具可用于在开发和单元测试期间调试您的驱动程序。</p>
<p>%WindowsSdkDir%\tools\x64\wiatest.htm</p>
<p>%WindowsSdkDir%\tools\x64\wiatest.htm</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows 图像处理跟踪文件查看器 (Wiatrcvw.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\Wiatrcvw.exe</p>
<p>%WindowsSdkDir%\tools\x86\Wiatrcvw.exe</p></td>
<td align="left"><p>显示 WIA 跟踪日志 （%windir%\debug\wia\wiatrace.log) 并允许您更改的每个模块的 WIA 跟踪参数。</p>
<p>%WindowsSdkDir%\tools\x64\Wiatrcvw.mht</p>
<p>%WindowsSdkDir%\tools\x64\Wiatrcvw.mht</p></td>
</tr>
</tbody>
</table>

 

### 技术：Windows 便携设备 (WPD) 驱动程序 <a name="tech-wpd"></a>

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">工具名称</th>
<th align="left">工具位置</th>
<th align="left">说明和帮助文件的位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WpdDeviceInspector (WpdDeviceInspector.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\WpdDeviceInspector.exe</p>
<p>%WindowsSdkDir%\tools\x86\WpdDeviceInspector.exe</p></td>
<td align="left"><p>查询 WPD 驱动程序，并生成全面的 HTML 报告，其中介绍了你的设备和其功能。 例如，您可以使用它来检索受支持的设备命令和对象的列表。 然后，此工具会生成支持每个对象的所有属性的列表。</p>
<p>WDK 文档：</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=106527" data-raw-source="[Windows Portable Devices](https://go.microsoft.com/fwlink/p/?linkid=106527)">Windows 便携设备</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=262664" data-raw-source="[WPD Driver Development Tools](https://go.microsoft.com/fwlink/p/?linkid=262664)">WPD 驱动程序开发工具</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WpdInfo (WpdInfo.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\WpdInfo.exe</p>
<p>%WindowsSdkDir%\tools\x86\WpdInfo.exe</p></td>
<td align="left"><p>例如执行常见 WPD 操作： 打开和关闭设备、 创建或删除设备上的对象和发出设备的命令。</p>
<p>WDK 文档：</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=106527" data-raw-source="[Windows Portable Devices](https://go.microsoft.com/fwlink/p/?linkid=106527)">Windows 便携设备</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=262664" data-raw-source="[WPD Driver Development Tools](https://go.microsoft.com/fwlink/p/?linkid=262664)">WPD 驱动程序开发工具</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Microsoft 网络监视器 (NetMon.exe)</p>
<p><strong>WDK 工具：</strong>否</p></td>
<td align="left"><p>下载 Microsoft 网络监视器 (NetMon.exe<a href="https://go.microsoft.com/fwlink/p/?linkid=248501" data-raw-source="[here](https://go.microsoft.com/fwlink/p/?linkid=248501)">此处</a>。</p></td>
<td align="left"><p>显示跟踪来自 WPD 组件的信息。 此工具将替代了以前版本的 WDK 中附带的 WpdMon.exe。</p>
<p>WDK 文档：</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=106527" data-raw-source="[Windows Portable Devices](https://go.microsoft.com/fwlink/p/?linkid=106527)">Windows 便携设备</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=262664" data-raw-source="[WPD Driver Development Tools](https://go.microsoft.com/fwlink/p/?linkid=262664)">WPD 驱动程序开发工具</a>，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh451296" data-raw-source="[Using the Network Monitor Tool](https://msdn.microsoft.com/library/windows/hardware/hh451296)">使用网络监视器工具</a>。</p></td>
</tr>
</tbody>
</table>

 

### 技术：打印机驱动程序 <a name="tech-printer"></a>

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">工具名称</th>
<th align="left">工具位置</th>
<th align="left">说明和帮助文件的位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>GPDCheck (Gpdcheck.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\gpdcheck.exe</p>
<p>%WindowsSdkDir%\tools\x86\gpdcheck.exe</p></td>
<td align="left"><p>验证语法正确的泛型打印机说明文件 (GPD)。</p>
<p>有关命令选项的信息，请键入</p>
<p><strong>gpdcheck /?</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>INFGate (Infgate.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\infgate.exe</p>
<p>%WindowsSdkDir%\tools\x86\infgate.exe.exe</p></td>
<td align="left"><p>验证打印机 INF 文件的符合性。</p>
<p>有关命令选项的信息，请键入</p>
<p><strong>infgate /?</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>isxps 合规 (isXPS.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\isxps\isxps.exe</p>
<p>%WindowsSdkDir%\tools\x86\isxps\isxps.exe</p></td>
<td align="left"><p>验证 XPS 和 OPC 规范 XPS 文件的符合性。</p>
<p>有关命令选项的信息，请键入</p>
<p><strong>isxps /?</strong> 在命令提示符窗口中。</p>
<p>有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=150004" data-raw-source="[isXPS Conformance Tool](https://go.microsoft.com/fwlink/p/?linkid=150004)">isxps 合规性工具</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Looksgood (Looksgood.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\looksgood.exe</p>
<p>%WindowsSdkDir%\tools\x86\looksgood.exe</p></td>
<td align="left"><p>验证 XPS 呈现引擎的正确性。</p>
<p>有关命令选项的信息，请键入</p>
<p><strong>looksgood /?</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>MakeNTF (Makentf.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\makentf.exe</p>
<p>%WindowsSdkDir%\tools\x86\makentf.exe</p></td>
<td align="left"><p>将 Adobe 字体指标 (AFM) 文件和东亚字体 AFM 文件转换为 Windows 字体文件 (.ntf)。</p>
<p>WDK 文档：</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546364" data-raw-source="[Converting AFM Files to NTF Files](https://msdn.microsoft.com/library/windows/hardware/ff546364)">将 AFM 文件转换为 NTF 文件</a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546366" data-raw-source="[Converting East Asian AFM Files to NTF Files](https://msdn.microsoft.com/library/windows/hardware/ff546366)">将东亚 AFM 文件转换为 NTF 文件</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>PPDCheck (Ppdcheck.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\ppdcheck.exe</p>
<p>%WindowsSdkDir%\tools\x86\ppdcheck.exe</p></td>
<td align="left"><p>验证语法正确的 PostScript 打印机说明文件 (PPD)。</p>
<p>有关命令选项的信息，请键入</p>
<p><strong>ppdcheck /?</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>PTConform (PTConform.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\PTConform.exe</p>
<p>%WindowsSdkDir%\tools\x86\PTConform.exe</p></td>
<td align="left"><p>验证符合打印架构为文档或打印功能打印票证。</p>
<p>有关命令选项的信息，请键入</p>
<p><strong>ptconform /？</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>XpsAnalyzer (XpsAnalyzer.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\XpsAnalyzer.exe</p>
<p>%WindowsSdkDir%\tools\x86\XpsAnalyzer.exe</p></td>
<td align="left"><p>分析 XML 纸张规范 (XPS) 文件与 XPS 1.0 规范的兼容性。</p>
<p>WDK 文档：</p>
<p><a href="xpsanalyzer.md" data-raw-source="[XpsAnalyzer](xpsanalyzer.md)">XpsAnalyzer</a></p></td>
</tr>
</tbody>
</table>

 

### 技术：传感器 <a name="tech-sensors"></a>

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">工具名称</th>
<th align="left">工具位置</th>
<th align="left">说明和帮助文件的位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>传感器诊断工具 (sensordiagnostictool.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64&lt;/p&gt;
<p>%WindowsSdkDir%\tools\x86&lt;/p&gt;</td>
<td align="left"><p>测试驱动程序、 固件和硬件的传感器和位置的功能。 若要测试数据检索、 事件处理、 报告间隔，请更改敏感度，检索属性的传感器和位置 API，将调用该工具。</p>
<p>WDK 文档：</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/hh780319" data-raw-source="[Testing sensor functionality with the Sensor Diagnostic Tool](https://msdn.microsoft.com/library/windows/hardware/hh780319)">使用传感器诊断工具测试传感器功能</a></p></td>
</tr>
</tbody>
</table>

 

### 技术：所有驱动程序 <a name="tech-all"></a>

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">工具名称</th>
<th align="left">工具位置</th>
<th align="left">说明和帮助文件的位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>BinPlace (Binplace.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x86\binplace.exe</p></td>
<td align="left"><p>管理大编码将文件移动项目，从可执行文件，提取符号并删除私有符号从符号文件。</p>
<p>WDK 文档：</p>
<p><a href="binplace.md" data-raw-source="[BinPlace](binplace.md)">BinPlace</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>驱动程序的代码分析</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>代码分析工具包含在 Visual Studio。 安装 WDK 时，被添加特定于驱动程序的组件。</p></td>
<td align="left"><p>静态验证工具，用于检测 C 和 c + + 编码错误。 此版本专门用于检测内核模式驱动程序中的错误。</p>
<div class="alert">
<strong>请注意</strong>  在以前版本的 WDK 中，此功能是 OACR 的一部分，也是可用作独立工具 PREfast for Drivers。 从 Visual Studio 2012 开始，该功能现已集成到 Visual Studio。
</div>
<div>
 
</div>
<p>WDK 文档：</p>
<p><a href="code-analysis-for-drivers.md" data-raw-source="[Code Analysis for Drivers](code-analysis-for-drivers.md)">驱动程序的代码分析</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>CertMgr (CertMgr.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\CertMgr.exe</p>
<p>%WindowsSdkDir%\bin\x86\CertMgr.exe</p></td>
<td align="left"><p>管理证书，证书信任列表 (Ctl) 和证书吊销列表 (Crl) 用于签署驱动程序和<a href="https://msdn.microsoft.com/library/windows/hardware/ff544840" data-raw-source="[driver packages](https://msdn.microsoft.com/library/windows/hardware/ff544840)">驱动程序包</a>。</p>
<p>WDK 文档：</p>
<p><a href="certmgr.md" data-raw-source="[&lt;strong&gt;CertMgr&lt;/strong&gt;](certmgr.md)"><strong>CertMgr</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>ChkINF</p>
<p><strong>WDK 工具：</strong>已弃用</p></td>
<td align="left"><p>上一个路径：</p>
<p>%WindowsSdkDir%\tools\x86\Chkinf</p></td>
<td align="left"><p>已弃用 ChkInf。 请改用<a href="infverif.md" data-raw-source="[InfVerif](infverif.md)">InfVerif</a></p>
<p>WDK 文档：</p>
<p><a href="infverif.md" data-raw-source="[InfVerif](infverif.md)">InfVerif</a></p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>计算机硬件标识工具 (ComputerHardwareIds.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p><strong>Windows 驱动程序工具包 (WDK) 8:</strong></p>
<p>%WindowsSdkDir%\tools\x64\ComputerHardwareIds.exe</p>
<p>%WindowsSdkDir%\tools\x86\ComputerHardwareIds.exe</p>
<p>WDKPath\tools\Other\ia64\ComputerHardwareIds.exe</p>
<p><strong>Windows 驱动程序工具包 (WDK) 8.1:</strong></p>
<p>%WindowsSdkDir%\bin\x64\ComputerHardwareIds.exe</p>
<p>%WindowsSdkDir%\bin\x86\ComputerHardwareIds.exe</p>
<p>%WindowsSdkDir%\bin\arm\ComputerHardwareIds.exe</p></td>
<td align="left"><p>计算机硬件 Id 派生自 SMBIOS 信息。</p>
<p>WDK 文档：</p>
<p><a href="computerhardwareids.md" data-raw-source="[ComputerHardwareIds](computerhardwareids.md)">ComputerHardwareIds</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>DC2WMIParser (DC2WMIParser.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\DC2WMIParser.exe</p>
<p>%WindowsSdkDir%\tools\x86\DC2WMIParser.exe</p></td>
<td align="left"><p>DC2WMIParser 是一种工具，收集由驱动程序验证程序创建的 WMI IRP 记录，并将此日志转换为文本文件。</p>
<p>文档：</p>
<p><a href="https://go.microsoft.com/fwlink/p/?LinkId=698758" data-raw-source="[IRP Logging](https://go.microsoft.com/fwlink/p/?LinkId=698758)">IRP 日志记录</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Dependency Walker (Depends.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\depends.exe</p>
<p>%WindowsSdkDir%\tools\x86\depends.exe</p></td>
<td align="left"><p>显示所需的树关系图中的应用程序的模块的依赖关系模式。 显示的内容包含大量详细信息，包括通过每个模块，该函数实际调用其他模块导出的函数和最小值的一组所需的模块加载和运行的文件。</p>
<p>在工具中，从<strong>Dependency Walker</strong>帮助菜单中，选择<strong>帮助主题</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DevCon (Devcon.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\devcon.exe</p>
<p>%WindowsSdkDir%\tools\x86\devcon.exe</p></td>
<td align="left"><p>命令行版本的设备管理器。 DevCon 启用、 禁用、 安装、 配置和删除本地计算机上的设备和本地和远程计算机上显示有关设备的详细的信息。</p>
<p>WDK 文档：</p>
<p><a href="devcon.md" data-raw-source="[DevCon](devcon.md)">DevCon</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>驱动程序 (Drivers.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\drivers.exe</p>
<p>%WindowsSdkDir%\tools\x86\drivers.exe</p></td>
<td align="left"><p>显示在计算机安装的所有驱动程序的列表。</p>
<p>WDK 文档：</p>
<p>无</p></td>
</tr>
<tr class="even">
<td align="left"><p>驱动程序验证程序 (Verifier.exe)</p>
<p><strong>WDK 工具：</strong>否</p></td>
<td align="left"><p>%Windir%\system32\verifier.exe</p></td>
<td align="left"><p>监视器内核模式驱动程序和图形驱动程序以检测非法的函数调用或可能会损坏系统的操作。 它可以使用者到各种压力和测试，以找到不正确的行为的驱动程序。</p>
<p>WDK 文档：</p>
<p><a href="driver-verifier.md" data-raw-source="[Driver Verifier](driver-verifier.md)">驱动程序验证程序</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>驱动程序验证日志 (DVL)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>要求使用 Microsoft Visual Studio 和 WDK。 从<strong>驱动程序</strong>菜单上，单击<strong>创建驱动程序验证日志...</strong></p></td>
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?linkid=227016" data-raw-source="[Windows Server 2012 Hardware Certification Program](https://go.microsoft.com/fwlink/p/?linkid=227016)">Windows Server 2012 的硬件认证计划</a>需要的所有适用的驱动程序提交的驱动程序验证日志 (DVL)。 DVL 包含来自代码分析和静态驱动程序验证程序日志文件的结果的摘要。 请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_verification_log" data-raw-source="[Creating a Driver Verification Log](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_verification_log)">创建驱动程序验证日志</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>增强的存储证书管理工具 (EhStorCertMgrCmd.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\ehstorcertmgrcmd.exe</p>
<p>%WindowsSdkDir%\tools\x86\ehstorcertmgrcmd.exe</p></td>
<td align="left"><p>管理符合 IEEE 1667 标准的 USB 存储设备上的证书。</p>
<p>WDK 文档：</p>
<p><a href="enhanced-storage-certificate-management-tool.md" data-raw-source="[Enhanced Storage Certificate Management Tool](enhanced-storage-certificate-management-tool.md)">增强的存储证书管理工具</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>事件和性能计数器清单生成器工具 (ECManGen.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\ECManGen.exe</p>
<p>%WindowsSdkDir%\bin\x86\ECManGen.exe</p></td>
<td align="left"><p>一个用于创建的事件或性能计数器清单工具 (*.man) 从零开始，无需使用的 XML 标记。 有关创建清单文件的信息，请参阅<a href="https://msdn.microsoft.com/library/windows/desktop/dd996930" data-raw-source="[Writing an Instrumentation Manifest (Windows)](https://msdn.microsoft.com/library/windows/desktop/dd996930)">检测清单 (Windows) 编写</a>部分以及<a href="adding-event-tracing-to-kernel-mode-drivers.md" data-raw-source="[Adding Event Tracing to Kernel-Mode Drivers](adding-event-tracing-to-kernel-mode-drivers.md)">添加到内核模式驱动程序的事件跟踪</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GUIDgen (Guidgen.exe)</p>
<p><strong>WDK 工具：</strong>否</p></td>
<td align="left"><p>下载位置<a href="https://go.microsoft.com/fwlink/p/?linkid=121586" data-raw-source="[Microsoft Exchange Server GUID Generator](https://go.microsoft.com/fwlink/p/?linkid=121586)">Microsoft Exchange Server GUID 生成器</a></p></td>
<td align="left"><p>生成可用于标识类、 对象和接口的全局唯一标识符 (GUID)。 生成的 GUID 复制到剪贴板中四种格式之一，以便可以将其插入到你的源代码。</p>
<p>GUIDGEN.doc （包含在下载包）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Inf2Cat (Inf2cat.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\inf2cat.exe</p>
<p>%WindowsSdkDir%\bin\x86\inf2cat.exe</p></td>
<td align="left"><p>确定是否<a href="https://msdn.microsoft.com/library/windows/hardware/ff544840" data-raw-source="[driver package's](https://msdn.microsoft.com/library/windows/hardware/ff544840)">驱动程序包</a>INF 文件可以是指定的 Windows 版本中，列表进行数字签名，并且如果是这样，将生成无符号<a href="https://msdn.microsoft.com/library/windows/hardware/ff537872" data-raw-source="[catalog files](https://msdn.microsoft.com/library/windows/hardware/ff537872)">编录文件</a>的可以应用到指定的 Windows版本。</p>
<p>WDK 文档：</p>
<p><a href="inf2cat.md" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](inf2cat.md)"><strong>Inf2Cat</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>InfVerif (InfVerif.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>c:\Program Files(x86)\Windows Kits\10\tools\arm\infverif.exe</p>
<p>c:\Program Files(x86)\Windows Kits\10\tools\arm64\infverif.exe</p>
<p>c:\Program Files(x86)\Windows Kits\10\tools\x86\infverif.exe</p>
<p>c:\Program Files(x86)\Windows Kits\10\tools\x64\infverif.exe</p>
<td align="left"><p>测试驱动程序 INF 文件。 除了报告 INF 语法问题，该工具将报告 INF 文件是否通用。</p>
<p>WDK 文档：</p>
<p><a href="infverif.md" data-raw-source="[InfVerif](infverif.md)">InfVerif</a></p></td>
</tr>

<tr class="even">
<td align="left"><p>MakeCat (MakeCat.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>WDKPath\bin\amd64\MakeCat.exe</p>
<p>WDKPath\bin\ia64\MakeCat.exe</p>
<p>WDKPath\bin\x86\MakeCat.exe</p></td>
<td align="left"><p>创建<a href="https://msdn.microsoft.com/library/windows/hardware/ff537872" data-raw-source="[catalog file](https://msdn.microsoft.com/library/windows/hardware/ff537872)">编录文件</a>有关<a href="https://msdn.microsoft.com/library/windows/hardware/ff544840" data-raw-source="[driver package](https://msdn.microsoft.com/library/windows/hardware/ff544840)">驱动程序包</a>。</p>
<p>WDK 文档：</p>
<p><a href="makecat.md" data-raw-source="[MakeCat](makecat.md)">MakeCat</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>MakeCert (MakeCert.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\MakeCert.exe</p>
<p>%WindowsSdkDir%\bin\x86\MakeCert.exe</p></td>
<td align="left"><p>创建系统测试的根键或另一个指定密钥签名的 X.509 证书。</p>
<p>WDK 文档：</p>
<p><a href="makecert.md" data-raw-source="[&lt;strong&gt;MakeCert&lt;/strong&gt;](makecert.md)"><strong>MakeCert</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>MSBuild (MSBuild.exe)</p>
<p><strong>WDK 工具：</strong>否</p></td>
<td align="left"><p>随 Visual Studio 安装</p></td>
<td align="left"><p>生成示例，驱动程序和 Microsoft WDK 中提供的关联的软件组件。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=262804" data-raw-source="[MSBuild]( https://go.microsoft.com/fwlink/p/?linkid=262804)">MSBuild</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>PnpCpu (PnPCpu.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\PnPCpu.exe</p>
<p>%WindowsSdkDir%\tools\x86\PnPCpu.exe</p></td>
<td align="left"><p>模拟正在运行的 Windows Server 2008 实例的处理器热的添加。</p>
<p>WDK 文档：</p>
<p><a href="pnpcpu.md" data-raw-source="[PNPCPU](pnpcpu.md)">PNPCPU</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>PnPUtil (PnPUtil.exe)</p>
<p><strong>WDK 工具：</strong>否</p></td>
<td align="left"><p>%Windir%\system32\pnputil.exe</p></td>
<td align="left"><p>安装或删除的命令行工具<a href="https://msdn.microsoft.com/library/windows/hardware/ff544840" data-raw-source="[driver packages](https://msdn.microsoft.com/library/windows/hardware/ff544840)">驱动程序包</a>从 Windows 驱动程序存储区。</p>
<p>此工具是在 Windows 7 和更高版本的 Windows 中可用。</p>
<p>WDK 文档：</p>
<p><a href="pnputil.md" data-raw-source="[PnPUtil](pnputil.md)">PnPUtil</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>PoolMon (Poolmon.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\poolmon.exe</p>
<p>%WindowsSdkDir%\tools\x86\poolmon.exe</p></td>
<td align="left"><p>显示操作系统收集从系统的分页和非分页内核池和用于终端服务会话使用的内存池的内存分配数据。 按池分配标记分组数据。</p>
<p>WDK 文档：</p>
<p><a href="poolmon.md" data-raw-source="[PoolMon](poolmon.md)">PoolMon</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>PowerCfg (PowerCfg.exe)</p>
<p><strong>WDK 工具：</strong>否</p></td>
<td align="left"><p>%Windir%\system32\powercfg.exe</p></td>
<td align="left"><p>用于评估系统能效命令行工具。</p>
<p>此工具是在 Windows 7 和更高版本的 Windows 中可用。</p>
<p>开发人员中心文档：</p>
<a href="http://download.microsoft.com/download/7/E/7/7E7662CF-CBEA-470B-A97E-CE7CE0D98DC2/PowerCfg.docx" data-raw-source="[Using PowerCfg to Evaluate System Energy Efficiency](http://download.microsoft.com/download/7/E/7/7E7662CF-CBEA-470B-A97E-CE7CE0D98DC2/PowerCfg.docx)">使用 PowerCfg 评估系统能效</a>
<p>有关命令选项的信息，请键入</p>
<p></p>
<p><strong>PowerCfg /?</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Pvk2Pfx (Pvk2Pfx.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\Pvk2Pfx.exe</p>
<p>%WindowsSdkDir%\bin\x86\Pvk2Pfx.exe</p></td>
<td align="left"><p>复制公钥和私钥信息包含在.spc、.cer 中，并.pvk 文件复制到个人信息交换 (.pfx) 文件中。</p>
<p>WDK 文档：</p>
<p><a href="pvk2pfx.md" data-raw-source="[&lt;strong&gt;Pvk2Pfx&lt;/strong&gt;](pvk2pfx.md)"><strong>Pvk2Pfx</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>PwrTest (Pwrtest.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\pwrtest.exe</p>
<p>%WindowsSdkDir%\tools\x86\pwrtest.exe</p></td>
<td align="left"><p>执行电源管理工具适用于 Windows 7 及更高版本，并记录电源管理的计算机的信息。</p>
<p>WDK 文档：</p>
<p><a href="pwrtest.md" data-raw-source="[PwrTest](pwrtest.md)">PwrTest</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>SignTool (SignTool.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\SignTool.exe</p>
<p>%WindowsSdkDir%\bin\x86\SignTool.exe</p></td>
<td align="left"><p>进行数字签名的文件，验证文件和文件的时间戳中的签名。</p>
<p>WDK 文档：</p>
<p><a href="signtool.md" data-raw-source="[&lt;strong&gt;SignTool&lt;/strong&gt;](signtool.md)"><strong>SignTool</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Stampinf (Stampinf.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\stampinf.exe</p>
<p>%WindowsSdkDir%\bin\x86\stampinf.exe</p></td>
<td align="left"><p>更新常见的 INF 文件指令，包括<strong>DriverVer</strong>指令。</p>
<p>WDK 文档：</p>
<p><a href="stampinf.md" data-raw-source="[Stampinf](stampinf.md)">Stampinf</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>静态驱动程序验证程序</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\SDV</p>
<p></p>
<div class="alert">
<strong>请注意</strong>  从启动 Static Driver Verifier<strong>驱动程序</strong>Visual Studio 菜单中的。
</div>
<div>
 
</div></td>
<td align="left"><p>一个静态验证工具驱动程序，可以系统地分析 Windows 驱动程序的源代码并确定该驱动程序是否正确交互与 Windows 操作系统内核。</p>
<p>WDK 文档：</p>
<p><a href="static-driver-verifier.md" data-raw-source="[Static Driver Verifier](static-driver-verifier.md)">静态驱动程序验证程序</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Tracefmt (Tracefmt.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\tracefmt.exe</p>
<p>%WindowsSdkDir%\bin\x86\tracefmt.exe</p></td>
<td align="left"><p>设置格式并显示从事件跟踪日志文件 (.etl) 或实时跟踪会话的跟踪消息。</p>
<p>WDK 文档：</p>
<p><a href="tracefmt.md" data-raw-source="[Tracefmt](tracefmt.md)">Tracefmt</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>跟踪日志 (Tracelog.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p><strong>WDK 8:</strong></p>
<p>%WindowsSdkDir%\tools\x64\tracelog.exe</p>
<p>%WindowsSdkDir%\tools\x86\tracelog.exe</p>
<p><strong>WDK 8.1:</strong></p>
<p>%WindowsSdkDir%\bin\x64\tracelog.exe</p>
<p>%WindowsSdkDir%\bin\x86\tracelog.exe</p>
<p>%WindowsSdkDir%\bin\arm\tracelog.exe</p></td>
<td align="left"><p>配置并控制从命令行跟踪会话。 测量时间花在延缓过程调用 (Dpc) 和中断服务例程 (Isr)。</p>
<p>WDK 文档：</p>
<p><a href="tracelog.md" data-raw-source="[Tracelog](tracelog.md)">Tracelog</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>TracePDB (Tracepdb.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\tracepdb.exe</p>
<p>%WindowsSdkDir%\bin\x86\tracepdb.exe</p></td>
<td align="left"><p>跟踪消息格式 (.tmf) 文件从完整或专用 PDB 符号文件为创建 WPP 跟踪提供程序。</p>
<p>WDK 文档：</p>
<p><a href="tracepdb.md" data-raw-source="[Tracepdb](tracepdb.md)">Tracepdb</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>TraceView (Traceview.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\TraceView.exe</p>
<p>%WindowsSdkDir%\tools\x86\TraceView.exe</p></td>
<td align="left"><p>配置和控制跟踪会话，并显示从实时跟踪会话和跟踪日志中的格式化的跟踪消息。 TraceView 具有图形用户界面和命令行界面和脚本编写针对批处理。</p>
<p>WDK 文档：</p>
<p><a href="traceview.md" data-raw-source="[TraceView](traceview.md)">TraceView</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>TraceWPP (Tracewpp.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\tracewpp.exe</p>
<p>%WindowsSdkDir%\bin\x86\tracewpp.exe</p></td>
<td align="left"><p>在运行 Windows 软件跟踪预处理器 (WPP)。</p>
<p>WDK 文档：</p>
<p><a href="wpp-preprocessor.md" data-raw-source="[WPP Preprocessor](wpp-preprocessor.md)">WPP 预处理器</a></p>
<p><a href="survey-of-software-tracing-tools.md" data-raw-source="[Survey of Software Tracing Tools](survey-of-software-tracing-tools.md)">软件跟踪工具的调查</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>WDF 测试人员</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64&lt;/p&gt;
<p>%WindowsSdkDir%\tools\x86&lt;/p&gt;</td>
<td align="left"><p>一组可用于测试、 验证和调试 WDF 驱动程序的工具。 该工具集提供一个 WMI 编程接口，可在脚本或编译的应用程序。</p>
<p>WDK 文档：</p>
<p><a href="wdftester--wdf-driver-testing-toolset.md" data-raw-source="[WdfTester: WDF Driver Testing Toolset](wdftester--wdf-driver-testing-toolset.md)">WdfTester:WDF 驱动程序测试工具集</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WDF 验证程序 (Wdfverifier.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\wdfverifier.exe</p>
<p>%WindowsSdkDir%\tools\x86\wdfverifier.exe</p></td>
<td align="left"><p>对于 KMDF 和 UMDF 驱动程序到框架的验证程序提供一个易于使用的界面。</p>
<p>WDK 文档：</p>
<p><a href="wdf-verifier-control-application.md" data-raw-source="[WDF Verifier Control Application](wdf-verifier-control-application.md)">WDF 验证程序控件应用程序</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Web 服务在设备上 (WSD) 基本互操作性工具 (WSDBIT)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p><strong>WSDBIT 客户端：</strong></p>
<p>%WindowsSdkDir%\tools\x64\wsdbit_client.exe</p>
<p>%WindowsSdkDir%\tools\x86\wsdbit_client.exe</p>
<p><strong>WSDBIT 服务器：</strong></p>
<p>%WindowsSdkDir%\tools\x64\wsdbit_server.exe</p>
<p>%WindowsSdkDir%\tools\x86\wsdbit_server.exe</p></td>
<td align="left"><p>验证的实现<a href="https://go.microsoft.com/fwlink/p/?linkid=81255" data-raw-source="[Device Profile for Web Services (DPWS)](https://go.microsoft.com/fwlink/p/?linkid=81255)">设备配置文件的 Web 服务 (DPWS)</a>配合 WSDAPI。</p>
<p>WDK 文档：</p>
<p><a href="wsdapi-basic-interoperability-tool.md" data-raw-source="[WSD Interoperability Tool](wsdapi-basic-interoperability-tool.md)">WSD 互操作性工具</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Winerror (Winerror.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\winerror.exe</p>
<p>%WindowsSdkDir%\tools\x86\winerror.exe</p></td>
<td align="left"><p>返回指定的错误 (Winerror.h) 或成功代码 (Ntstatus.h) 的错误消息标识符和映射信息。</p>
<p>有关命令选项的信息，请键入</p>
<p><strong>winerror /?</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>WMIMofCk (Wmimofck.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x86\wmimofck.exe</p></td>
<td align="left"><p>WDK 文档：</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565588" data-raw-source="[Using wmimofck.exe](https://msdn.microsoft.com/library/windows/hardware/ff565588)">使用 wmimofck.exe</a></p>
<p>有关命令选项的信息，请键入</p>
<p><strong>wmimofck -?</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>一些 (Wsdcodegen.exe)</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\wsdcodegen.exe</p>
<p>%WindowsSdkDir%\bin\x86\wsdcodegen.exe</p></td>
<td align="left"><p>自动生成代理和存根 （stub） 基于 Web 服务约定。 首先，此工具可用于创建客户端应用程序。 但是，可以将它用于测试或用于创建用户模式驱动程序。</p>
<p>验证可用于 WMI 类、 属性、 方法和二进制的 MOF 文件 (.bmf) 中指定的事件。 生成 MOF 支持文件。</p>
<p>Windows SDK:</p>
<p>请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=81407" data-raw-source="[Web Services on Devices](https://go.microsoft.com/fwlink/p/?linkid=81407)">设备上的 Web 服务</a>部分</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WSDDebug_client 和 WSDDebug_host</p>
<p><strong>WDK 工具：</strong>是</p></td>
<td align="left"><p><strong>调试客户端：</strong></p>
<p>%WindowsSdkDir%\bin\x64\WSDDebug_client.exe</p>
<p>%WindowsSdkDir%\bin\x86\WSDDebug_client.exe</p>
<p><strong>调试主机：</strong></p>
<p>%WindowsSdkDir%\bin\x64\WSDDebug_host.exe</p>
<p>%WindowsSdkDir%\bin\x86\WSDDebug_host.exe</p></td>
<td align="left"><p>这些工具是软设备和客户端，可用于对设备或应用程序进行故障排除。</p>
<p>Windows SDK:</p>
<p>请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=81407" data-raw-source="[Web Services on Devices](https://go.microsoft.com/fwlink/p/?linkid=81407)">设备上的 Web 服务</a>部分</p></td>
</tr>
</tbody>
</table>

 

### 什么是 Windows 8.1 的 WDK 中的新增功能 <a name="what-s-new-in-the-wdk-for-windows8-1"></a>

以下工具已添加或已改变的 WDK 8.1:

-   HCK 测试套件 (请参阅[如何测试在运行时使用 Visual Studio 的驱动程序](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)并[如何在 WDK 8.1 中运行 HCK 测试套件](https://msdn.microsoft.com/windows-drivers/develop/run_the_hck_test_suites_in_the_wdk)。)

-   [驱动程序验证程序](driver-verifier.md)— 现在有四个新选项来在 Windows 驱动程序中检测错误。
-   [PwrTest](pwrtest.md)-更新的文档，新的测试方案，包括支持连接待机电源状态。
-   [Tracelog](tracelog.md)— 新的选项。

### 什么是适用于 Windows 8 WDK 中的新增功能 <a name="what-s-new-in-the-wdk-for-windows8"></a>

已添加到 Windows 8 的 WDK 以下工具：

-   蓝牙查询记录验证程序 (Sdpverify.exe)

-   设备基础测试 (请参阅[如何测试在运行时使用 Visual Studio 的驱动程序](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)并[如何选择和配置设备基础测试](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)。

-   传感器诊断工具 (sensordiagnostictool.exe)

### 更改的内容在 WDK 中针对 Windows 8 <a name="what-s-changed-in-the-wdk-for-windows8"></a>
以下工具是 Microsoft WDK 适用于 Windows 7 中，但不是包括在 Windows 8 的 WDK。

-   Windows 生物识别框架工具 （BioTest.exe，WBDIDriverTest.exe）

-   设备路径试验程序 (devpathexer.exe)。 现在的设备基础的一部分模糊测试。

-   IoSpy 和 IoAttack （IoSpyCmd.exe，IoAttack.exe）。 现在属于设备基本测试。

-   Kernrate (Kernrate.exe) Kernrate 不再受支持。 请改用[Windows 性能分析工具包](https://go.microsoft.com/fwlink/p/?linkid=294280)。

-   Microsoft 自动代码评审 (OACR) （驱动程序组件现在的一部分在 Visual Studio 中的代码分析工具。）

-   Plug and Play 驱动程序测试 (pnpdtest.exe)。 现在属于设备基本测试。

-   ProCalc

-   WWAN 驱动程序测试应用 (wwandrivertestapp.exe)

### <a name="supported-platforms"></a>受支持的平台

WDK 8.1 支持这些版本的 Windows 运行的驱动程序开发：

-   Windows 8.1 和 Windows 8

-   Windows Server 2012 R2 和 Windows Server 2012

-   Windows 7

-   Windows Server 2008 R2

-   对于 Windows Vista （包括 SP1 和 SP2） 中，必须使用 WDK 8。 对于 Windows XP 中，必须使用 WDK 7。

可以在这些版本的 Windows 上运行集成的 Visual Studio 驱动程序开发环境。

-   Windows 8.1 和 Windows 8

-   Windows Server 2012 R2 和 Windows Server 2012

-   Windows 7

-   Windows Server 2008 R2

 

 

