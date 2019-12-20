---
title: Windows 驱动程序工具包工具的索引
description: Windows 驱动程序工具包工具的索引
ms.assetid: 26db88c4-8fb8-4308-ab8a-1a1eef5e19d8
keywords:
- 禁用程序工具
- DbgCon 工具
- Sniffir 工具
- Sledge 工具
- 调用使用情况验证程序工具
- CUV 工具
- 工具 WDK，已列出
- 驱动程序开发工具 WDK，已列出
- 睡眠状态选择器
- sleeper
- Acpislp
- 手动电源状态更改测试
- Guidgen.exe WDK
- GUID 生成器 WDK
- Guidgen.exe WDK
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 33cdaf80ef88dd61f3f8c1971366bc7a0058ce0d
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209457"
---
# <a name="index-of-windows-driver-kit-tools"></a>Windows 驱动程序工具包工具的索引


本主题提供有关 Windows 驱动程序工具包（WDK）中包含的工具的基本信息。 本主题还包括对驱动程序开发有用的其他工具的参考。 这些其他工具要么作为操作系统的一部分提供，要么作为单独的下载提供。 有关每个工具的详细信息，请参阅本主题介绍该工具的文档。

有关如何获取最新 WDK 的信息，请参阅[Windows 驱动程序工具包（WDK）](https://go.microsoft.com/fwlink/p/?linkid=261797)。

本主题包括以下内容：

-   [WDK 工具的索引](#index-of-wdk-tools)
-   [WDK 中用于 Windows 8.1 的新增功能](#what-s-new-in-the-wdk-for-windows8-1)
-   [Windows 8 的 WDK 新增功能](#what-s-new-in-the-wdk-for-windows8)
-   [适用于 Windows 8 的 WDK 中发生了哪些更改](#what-s-changed-in-the-wdk-for-windows8)
-   [支持的平台](#supported-platforms)

### <a name="index-of-wdk-tools"></a>WDK 工具的索引

下表中的信息描述了适用于 Windows 驱动程序开发人员的工具。 工具列表包括随 WDK 提供的工具（由**wdk 工具**字段指示），还包括一些单独提供或随 Windows 一起安装的工具。 [所有](#tech-all)驱动程序通常都列出可用于所有驱动程序的工具。 特定于技术的工具组合在一起，例如，特定于[Windows 便携设备（WPD）驱动程序](#tech-wpd)或[传感器](#tech-sensors)的工具。

-   [音频/视频驱动程序](#tech-audio-video)
-   [蓝牙驱动程序](#tech-bluetooth)
-   [Windows 图像获取（WIA）驱动程序](#tech_wia)
-   [Windows 便携设备（WPD）驱动程序](#tech-wpd)
-   [打印机驱动程序](#tech-printer)
-   [传感器](#tech-sensors)
-   [所有驱动程序](#tech-all)

**请注意**  Visual Studio 环境变量% WindowsSdkDir% 表示安装了此版本的 WDK 的 Windows 工具包目录的路径，例如，C：\\Program Files （x86）\\Windows 工具包\\8.1。

 

### 技术：音频/视频驱动程序<a name="tech-audio-video"></a>

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
<th align="left">说明和帮助文件位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>显示颜色校准工具（Dccw）</p>
<p><strong>WDK 工具：</strong>不</p></td>
<td align="left"><p>%Windir%\System32\Dccw.exe</p></td>
<td align="left"><p>一种校准工具，它使用户能够调整其显示颜色，使其更接近 Windows 和万维网国际标准红-绿-蓝（sRGB）颜色空间。</p>
</tr>
<tr class="even">
<td align="left"><p>GraphEdt （Graphedt）</p>
<p><strong>WDK 中的工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\graphedt.exe</p>
<p>%WindowsSdkDir%\tools\x64\graphedt.exe</p></td>
<td align="left"><p>生成筛选器关系图以测试流式传输音频/视频捕获驱动程序。</p>
<p>关于</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=9230" data-raw-source="[Overview of GraphEdit](https://go.microsoft.com/fwlink/p/?linkid=9230)">GraphEdit 概述</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSStudio （KsStudio）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\KsStudio.exe</p>
<p>%WindowsSdkDir%\tools\x64\KsStudio.exe</p>
<div class="alert">
<strong>请注意</strong>   此工具必须由具有管理员权限的用户运行。
</div>
<div>
 
</div></td>
<td align="left"><p>此工具可以构造筛选器图的图形表示形式，该图显示了筛选器与筛选器的内部节点之间的 pin 到针连接。</p>
<p>%WindowsSdkDir%\tools\x86\KsStudio.chm</p>
<p>%WindowsSdkDir%\tools\x64\KsStudio.chm</p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-testing-and-debugging" data-raw-source="[AVStream Testing and Debugging](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-testing-and-debugging)">AVStream 测试和调试</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>USB 设备查看器（Usbview）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\Usbview.exe</p>
<p>%WindowsSdkDir%\tools\x64\Usbview.exe</p></td>
<td align="left"><p>枚举 USB 主机控制器、USB 集线器和连接的 USB 设备，并可以从注册表查询设备信息，并通过 USB 请求将设备查询到设备。</p>
<p>可以从代码库中获取 USB 设备查看器的源代码，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=256205" data-raw-source="[USBVIEW Sample Application](https://go.microsoft.com/fwlink/p/?linkid=256205)">USBVIEW 示例应用程序</a>。</p></td>
</tr>
</tbody>
</table>

 

### 技术：蓝牙驱动程序<a name="tech-bluetooth"></a>

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
<th align="left">说明和帮助文件位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>蓝牙查询记录验证程序（Sdpverify）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\Sdpverifiy.exe</p>
<p>%WindowsSdkDir%\tools\x64\Sdpverifiy.exe</p></td>
<td align="left"><p>显示 Windows 解释蓝牙设备的查询记录。</p>
<p>WDK 文档：</p>
<p><a href="bluetooth-inquiry-record-verifier.md" data-raw-source="[Bluetooth Inquiry Record Verifier](bluetooth-inquiry-record-verifier.md)">蓝牙查询记录验证程序</a></p></td>
</tr>
</tbody>
</table>

 

### 技术： Windows 图像获取（WIA）驱动程序<a name="tech_wia"></a>

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
<th align="left">说明和帮助文件位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WIADbgCfg （Wiadbgcfg）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\wiadbgcfg.exe</p>
<p>%WindowsSdkDir%\tools\x64\wiadbgcfg.exe</p></td>
<td align="left"><p>为 WIA 驱动程序启用日志记录（Windows Server 2008 和更高版本的 Windows）。</p>
<div class="alert">
<strong>请注意</strong>，   适用于 Windows 的早期版本，请使用 WIALogCfg。
</div>
<div>
 
</div>
<p>%WindowsSdkDir%\tools\x86\wiadbgcfg.htm</p>
<p>%WindowsSdkDir%\tools\x64\wiadbgcfg.htm</p></td>
</tr>
<tr class="even">
<td align="left"><p>WIAInfo2 （Wiainfo2）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\wiainfo2.exe</p>
<p>%WindowsSdkDir%\tools\x64\wiainfo2.exe</p></td>
<td align="left"><p>显示 WIA 项树，以便您可以查看和编辑 WIA 设备驱动程序属性。</p>
<p>%WindowsSdkDir%\tools\x86\wiainfo2.htm</p>
<p>%WindowsSdkDir%\tools\x64\wiainfo2.htm</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WIAPreview （Wiapreview）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\wiapreview.exe</p>
<p>%WindowsSdkDir%\tools\x86\wiapreview.exe</p></td>
<td align="left"><p>演示如何使用 WIA 预览组件和驱动程序的分段筛选器。</p>
<p>%WindowsSdkDir%\tools\x64\wiapreview.htm</p>
<p>%WindowsSdkDir%\tools\x86\wiapreview.htm</p></td>
</tr>
<tr class="even">
<td align="left"><p>WIATest （Wiatest）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\wiatest.exe</p>
<p>%WindowsSdkDir%\tools\x86\wiatest.exe</p></td>
<td align="left"><p>显示由驱动程序、由驱动程序公开的 Windows 图像获取（WIA）属性以及每个属性的当前值创建的项树。 您可以使用此工具在开发和单元测试过程中调试驱动程序。</p>
<p>%WindowsSdkDir%\tools\x64\wiatest.htm</p>
<p>%WindowsSdkDir%\tools\x64\wiatest.htm</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows 映像跟踪文件查看器（Wiatrcvw）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\Wiatrcvw.exe</p>
<p>%WindowsSdkDir%\tools\x86\Wiatrcvw.exe</p></td>
<td align="left"><p>显示 WIA 跟踪日志（%WINDIR%\Debug\WIA\wiatrace.log），并允许您更改每个模块的 WIA 跟踪参数。</p>
<p>%WindowsSdkDir%\tools\x64\Wiatrcvw.mht</p>
<p>%WindowsSdkDir%\tools\x64\Wiatrcvw.mht</p></td>
</tr>
</tbody>
</table>

 

### 技术： Windows 便携设备（WPD）驱动程序<a name="tech-wpd"></a>

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
<th align="left">说明和帮助文件位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WpdDeviceInspector （WpdDeviceInspector）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\WpdDeviceInspector.exe</p>
<p>%WindowsSdkDir%\tools\x86\WpdDeviceInspector.exe</p></td>
<td align="left"><p>查询 WPD 驱动程序，并生成全面的 HTML 报告，用于描述设备及其功能。 例如，你可以使用它来检索受支持的设备命令和对象的列表。 此工具将生成每个对象支持的所有属性的列表。</p>
<p>WDK 文档：</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=106527" data-raw-source="[Windows Portable Devices](https://go.microsoft.com/fwlink/p/?linkid=106527)">Windows 便携设备</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=262664" data-raw-source="[WPD Driver Development Tools](https://go.microsoft.com/fwlink/p/?linkid=262664)">WPD 驱动程序开发工具</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WpdInfo （WpdInfo）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\WpdInfo.exe</p>
<p>%WindowsSdkDir%\tools\x86\WpdInfo.exe</p></td>
<td align="left"><p>执行常见的 WPD 操作，例如：打开和关闭设备、在设备上创建或删除对象以及发出设备命令。</p>
<p>WDK 文档：</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=106527" data-raw-source="[Windows Portable Devices](https://go.microsoft.com/fwlink/p/?linkid=106527)">Windows 便携设备</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=262664" data-raw-source="[WPD Driver Development Tools](https://go.microsoft.com/fwlink/p/?linkid=262664)">WPD 驱动程序开发工具</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Microsoft 网络监视器（NetMon）</p>
<p><strong>WDK 工具：</strong>不</p></td>
<td align="left"><p>下载 Microsoft 网络监视器（<a href="https://go.microsoft.com/fwlink/p/?linkid=248501" data-raw-source="[here](https://go.microsoft.com/fwlink/p/?linkid=248501)">此处</a>为 NetMon。</p></td>
<td align="left"><p>显示 WPD 组件中的跟踪信息。 此工具取代了以前版本的 WDK 中随附的 WpdMon。</p>
<p>WDK 文档：</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=106527" data-raw-source="[Windows Portable Devices](https://go.microsoft.com/fwlink/p/?linkid=106527)">Windows 便携设备</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=262664" data-raw-source="[WPD Driver Development Tools](https://go.microsoft.com/fwlink/p/?linkid=262664)">WPD 驱动程序开发工具</a>，请参阅<a href="https://docs.microsoft.com/previous-versions/hh451296(v=vs.85)" data-raw-source="[Using the Network Monitor Tool](https://docs.microsoft.com/previous-versions/hh451296(v=vs.85))">使用网络监视器工具</a>。</p></td>
</tr>
</tbody>
</table>

 

### 技术：打印机驱动程序<a name="tech-printer"></a>

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
<th align="left">说明和帮助文件位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>GPDCheck （Gpdcheck）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\gpdcheck.exe</p>
<p>%WindowsSdkDir%\tools\x86\gpdcheck.exe</p></td>
<td align="left"><p>验证一般打印机说明文件（GPD）的语法正确性。</p>
<p>有关命令选项的信息，请键入</p>
<p><strong>gpdcheck /?</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>INFGate （Infgate）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\infgate.exe</p>
<p>%WindowsSdkDir%\tools\x86\infgate.exe.exe</p></td>
<td align="left"><p>验证打印机 INF 文件的一致性。</p>
<p>有关命令选项的信息，请键入</p>
<p><strong>infgate /?</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Isxps.exe （Isxps.exe）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\isxps\isxps.exe</p>
<p>%WindowsSdkDir%\tools\x86\isxps\isxps.exe</p></td>
<td align="left"><p>验证 XPS 文件与 XPS 和 OPC 规范的符合性。</p>
<p>有关命令选项的信息，请键入</p>
<p><strong>isxps.exe/？</strong> 在命令提示符窗口中。</p>
<p>有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=150004" data-raw-source="[isXPS Conformance Tool](https://go.microsoft.com/fwlink/p/?linkid=150004)">Isxps.exe 一致性工具</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Looksgood （Looksgood）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\looksgood.exe</p>
<p>%WindowsSdkDir%\tools\x86\looksgood.exe</p></td>
<td align="left"><p>验证 XPS 呈现引擎的正确性。</p>
<p>有关命令选项的信息，请键入</p>
<p><strong>looksgood /?</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>MakeNTF （Makentf）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\makentf.exe</p>
<p>%WindowsSdkDir%\tools\x86\makentf.exe</p></td>
<td align="left"><p>将 Adobe 字体指标（AFM）文件和中文字体 AFM 文件转换为 Windows 字体文件（. contoso.ntf）。</p>
<p>WDK 文档：</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/print/converting-afm-files-to-ntf-files" data-raw-source="[Converting AFM Files to NTF Files](https://docs.microsoft.com/windows-hardware/drivers/print/converting-afm-files-to-ntf-files)">将 AFM 文件转换为 CONTOSO.NTF 文件</a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/print/converting-east-asian-afm-files-to-ntf-files" data-raw-source="[Converting East Asian AFM Files to NTF Files](https://docs.microsoft.com/windows-hardware/drivers/print/converting-east-asian-afm-files-to-ntf-files)">将东亚 AFM 文件转换为 CONTOSO.NTF 文件</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>PPDCheck （Ppdcheck）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\ppdcheck.exe</p>
<p>%WindowsSdkDir%\tools\x86\ppdcheck.exe</p></td>
<td align="left"><p>验证 PostScript 打印机说明文件（PPD）的语法正确性。</p>
<p>有关命令选项的信息，请键入</p>
<p><strong>ppdcheck /?</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>PTConform （PTConform）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\PTConform.exe</p>
<p>%WindowsSdkDir%\tools\x86\PTConform.exe</p></td>
<td align="left"><p>验证打印票证或打印功能文档是否符合打印架构。</p>
<p>有关命令选项的信息，请键入</p>
<p><strong>ptconform /?</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>XpsAnalyzer （XpsAnalyzer）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\XpsAnalyzer.exe</p>
<p>%WindowsSdkDir%\tools\x86\XpsAnalyzer.exe</p></td>
<td align="left"><p>分析 XML 纸张规范（XPS）文件，以与 XPS 1.0 规范兼容。</p>
<p>WDK 文档：</p>
<p><a href="xpsanalyzer.md" data-raw-source="[XpsAnalyzer](xpsanalyzer.md)">XpsAnalyzer</a></p></td>
</tr>
</tbody>
</table>

 

### 技术：传感器<a name="tech-sensors"></a>

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
<th align="left">说明和帮助文件位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>传感器诊断工具（sensordiagnostictool）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64&lt;/p&gt;
<p>%WindowsSdkDir%\tools\x86&lt;/p&gt;</td>
<td align="left"><p>测试传感器和位置功能的驱动程序、固件和硬件。 该工具调用传感器和位置 API 来测试数据检索、事件处理、报告间隔、更改敏感度、属性检索。</p>
<p>WDK 文档：</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/sensors/the-sensor-diagnostic-tool" data-raw-source="[Testing sensor functionality with the Sensor Diagnostic Tool](https://docs.microsoft.com/windows-hardware/drivers/sensors/the-sensor-diagnostic-tool)">通过传感器诊断工具测试传感器功能</a></p></td>
</tr>
</tbody>
</table>

 

### 技术：所有驱动程序<a name="tech-all"></a>

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
<th align="left">说明和帮助文件位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>BinPlace （Binplace）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x86\binplace.exe</p></td>
<td align="left"><p>通过移动文件、从可执行文件提取符号以及从符号文件中删除私有符号，管理大型编码项目。</p>
<p>WDK 文档：</p>
<p><a href="binplace.md" data-raw-source="[BinPlace](binplace.md)">BinPlace</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>驱动程序的代码分析</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>代码分析工具包含在 Visual Studio 中。 安装 WDK 时，会添加驱动程序特定的组件。</p></td>
<td align="left"><p>检测 C 和C++编码错误的静态验证工具。 此版本专用于检测内核模式驱动程序中的错误。</p>
<div class="alert">
<strong>请注意</strong>，在以前版本的 WDK 中  ，此功能是 OACR 的一部分，也可以作为独立工具 PREfast 用于驱动程序。 从 Visual Studio 2012 开始，该功能现已集成到 Visual Studio 中。
</div>
<div>
 
</div>
<p>WDK 文档：</p>
<p><a href="code-analysis-for-drivers.md" data-raw-source="[Code Analysis for Drivers](code-analysis-for-drivers.md)">驱动程序的代码分析</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Certmgr.msc （Certmgr.msc）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\CertMgr.exe</p>
<p>%WindowsSdkDir%\bin\x86\CertMgr.exe</p></td>
<td align="left"><p>管理证书、证书信任列表（Ctl）和证书吊销列表（Crl），用于签署驱动程序和<a href="https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages" data-raw-source="[driver packages](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)">驱动程序包</a>。</p>
<p>WDK 文档：</p>
<p><a href="certmgr.md" data-raw-source="[&lt;strong&gt;CertMgr&lt;/strong&gt;](certmgr.md)"><strong>Certmgr.msc</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>ChkINF</p>
<p><strong>WDK 工具：</strong>弃用</p></td>
<td align="left"><p>先前路径：</p>
<p>%WindowsSdkDir%\tools\x86\Chkinf</p></td>
<td align="left"><p>ChkInf 已被弃用。 改为使用<a href="infverif.md" data-raw-source="[InfVerif](infverif.md)">InfVerif</a></p>
<p>WDK 文档：</p>
<p><a href="infverif.md" data-raw-source="[InfVerif](infverif.md)">InfVerif</a></p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>计算机硬件标识工具（ComputerHardwareIds）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p><strong>Windows 驱动程序工具包（WDK）8：</strong></p>
<p>%WindowsSdkDir%\tools\x64\ComputerHardwareIds.exe</p>
<p>%WindowsSdkDir%\tools\x86\ComputerHardwareIds.exe</p>
<p>WDKPath\tools\Other\ia64\ComputerHardwareIds.exe</p>
<p><strong>Windows 驱动程序工具包（WDK）8.1：</strong></p>
<p>%WindowsSdkDir%\bin\x64\ComputerHardwareIds.exe</p>
<p>%WindowsSdkDir%\bin\x86\ComputerHardwareIds.exe</p>
<p>%WindowsSdkDir%\bin\arm\ComputerHardwareIds.exe</p></td>
<td align="left"><p>从 SMBIOS 信息派生计算机硬件 Id。</p>
<p>WDK 文档：</p>
<p><a href="computerhardwareids.md" data-raw-source="[ComputerHardwareIds](computerhardwareids.md)">ComputerHardwareIds</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>DC2WMIParser （DC2WMIParser）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\DC2WMIParser.exe</p>
<p>%WindowsSdkDir%\tools\x86\DC2WMIParser.exe</p></td>
<td align="left"><p>DC2WMIParser 是一种工具，用于收集驱动程序验证器创建的 WMI IRP 记录，并将此日志转换为文本文件。</p>
<p>关于</p>
<p><a href="https://go.microsoft.com/fwlink/p/?LinkId=698758" data-raw-source="[IRP Logging](https://go.microsoft.com/fwlink/p/?LinkId=698758)">IRP 日志记录</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>依赖关系查看（取决于 .exe）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\depends.exe</p>
<p>%WindowsSdkDir%\tools\x86\depends.exe</p></td>
<td align="left"><p>显示树关系图中应用程序所需的模块的依赖关系模式。 显示内容包括很多详细信息，包括每个模块导出的函数、其他模块实际调用的函数和加载和运行模块所需的最小文件集。</p>
<p>在该工具中，从<strong>依赖关系</strong>查看 "帮助" 菜单中选择 "<strong>帮助主题</strong>"。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DevCon （Devcon）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\devcon.exe</p>
<p>%WindowsSdkDir%\tools\x86\devcon.exe</p></td>
<td align="left"><p>设备管理器的命令行版本。 DevCon 启用、禁用、安装、配置和删除本地计算机上的设备，并显示有关本地和远程计算机上的设备的详细信息。</p>
<p>WDK 文档：</p>
<p><a href="devcon.md" data-raw-source="[DevCon](devcon.md)">DevCon</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>驱动程序（驱动程序）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\drivers.exe</p>
<p>%WindowsSdkDir%\tools\x86\drivers.exe</p></td>
<td align="left"><p>显示计算机上安装的所有驱动程序的列表。</p>
<p>WDK 文档：</p>
<p>无</p></td>
</tr>
<tr class="even">
<td align="left"><p>驱动程序验证程序（Verifier）</p>
<p><strong>WDK 工具：</strong>不</p></td>
<td align="left"><p>%Windir%\system32\verifier.exe</p></td>
<td align="left"><p>监视内核模式驱动程序和图形驱动程序，以检测可能损坏系统的非法函数调用或操作。 它可以将驱动程序用于各种强调和测试，以找出不正确的行为。</p>
<p>WDK 文档：</p>
<p><a href="driver-verifier.md" data-raw-source="[Driver Verifier](driver-verifier.md)">驱动程序验证程序</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>驱动程序验证日志（DVL）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>需要 Microsoft Visual Studio 和 WDK。 在 "<strong>驱动程序</strong>" 菜单中，单击 "<strong>创建驱动程序验证日志 ...</strong> "。</p></td>
<td align="left"><p>对于所有适用的驱动程序提交， <a href="https://go.microsoft.com/fwlink/p/?linkid=227016" data-raw-source="[Windows Server 2012 Hardware Certification Program](https://go.microsoft.com/fwlink/p/?linkid=227016)">Windows Server 2012 硬件认证计划</a>需要驱动程序验证日志（DVL）。 DVL 包含代码分析的结果和静态驱动程序验证程序日志文件的摘要。 请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Creating a Driver Verification Log](https://docs.microsoft.com/windows-hardware/drivers)">创建驱动程序验证日志</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>增强的存储证书管理工具（EhStorCertMgrCmd）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\ehstorcertmgrcmd.exe</p>
<p>%WindowsSdkDir%\tools\x86\ehstorcertmgrcmd.exe</p></td>
<td align="left"><p>管理兼容 IEEE 1667 标准的 USB 存储设备上的证书。</p>
<p>WDK 文档：</p>
<p><a href="enhanced-storage-certificate-management-tool.md" data-raw-source="[Enhanced Storage Certificate Management Tool](enhanced-storage-certificate-management-tool.md)">增强的存储证书管理工具</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>事件和性能计数器清单生成器工具（ECManGen）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\ECManGen.exe</p>
<p>%WindowsSdkDir%\bin\x86\ECManGen.exe</p></td>
<td align="left"><p>用于从头开始创建事件或性能计数器清单（* man）的工具，无需使用 XML 标记。 有关创建清单文件的信息，请参阅<a href="https://docs.microsoft.com/windows/desktop/WES/writing-an-instrumentation-manifest" data-raw-source="[Writing an Instrumentation Manifest (Windows)](https://docs.microsoft.com/windows/desktop/WES/writing-an-instrumentation-manifest)">编写检测清单（Windows）</a>部分和<a href="adding-event-tracing-to-kernel-mode-drivers.md" data-raw-source="[Adding Event Tracing to Kernel-Mode Drivers](adding-event-tracing-to-kernel-mode-drivers.md)">向内核模式驱动程序添加事件跟踪</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Guidgen.exe （Guidgen.exe）</p>
<p><strong>WDK 工具：</strong>不</p></td>
<td align="left"><p>可从<a href="https://go.microsoft.com/fwlink/p/?linkid=121586" data-raw-source="[Microsoft Exchange Server GUID Generator](https://go.microsoft.com/fwlink/p/?linkid=121586)">Microsoft Exchange SERVER GUID 生成器</a>下载</p></td>
<td align="left"><p>生成全局唯一标识符（GUID），您可以使用它们来标识类、对象和接口。 生成的 GUID 将以四种格式之一复制到剪贴板，以便可以将其插入到源代码中。</p>
<p>GUIDGEN.EXE （包含在下载包中）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Inf2Cat （Inf2cat）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\inf2cat.exe</p>
<p>%WindowsSdkDir%\bin\x86\inf2cat.exe</p></td>
<td align="left"><p>确定是否可以为指定的 Windows 版本列表对<a href="https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages" data-raw-source="[driver package's](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)">驱动程序包的</a>INF 文件进行数字签名，如果是，则将生成适用于指定 windows 版本的未签名的<a href="https://docs.microsoft.com/windows-hardware/drivers/install/catalog-files" data-raw-source="[catalog files](https://docs.microsoft.com/windows-hardware/drivers/install/catalog-files)">目录文件</a>。</p>
<p>WDK 文档：</p>
<p><a href="inf2cat.md" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](inf2cat.md)"><strong>Inf2Cat</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>InfVerif （InfVerif）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>c:\Program Files （x86） \Windows Kits\10\tools\arm\infverif.exe</p>
<p>c:\Program Files （x86） \Windows Kits\10\tools\arm64\infverif.exe</p>
<p>c:\Program Files （x86） \Windows Kits\10\tools\x86\infverif.exe</p>
<p>c:\Program Files （x86） \Windows Kits\10\tools\x64\infverif.exe</p>
<td align="left"><p>测试驱动程序 INF 文件。 除了报告 INF 语法问题外，该工具还报告 INF 文件是否是通用的。</p>
<p>WDK 文档：</p>
<p><a href="infverif.md" data-raw-source="[InfVerif](infverif.md)">InfVerif</a></p></td>
</tr>

<tr class="even">
<td align="left"><p>MakeCat （MakeCat）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>WDKPath\bin\amd64\MakeCat.exe</p>
<p>WDKPath\bin\ia64\MakeCat.exe</p>
<p>WDKPath\bin\x86\MakeCat.exe</p></td>
<td align="left"><p>为<a href="https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages" data-raw-source="[driver package](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)">驱动程序包</a>创建<a href="https://docs.microsoft.com/windows-hardware/drivers/install/catalog-files" data-raw-source="[catalog file](https://docs.microsoft.com/windows-hardware/drivers/install/catalog-files)">编录文件</a>。</p>
<p>WDK 文档：</p>
<p><a href="makecat.md" data-raw-source="[MakeCat](makecat.md)">MakeCat</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>MakeCert （MakeCert）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\MakeCert.exe</p>
<p>%WindowsSdkDir%\bin\x86\MakeCert.exe</p></td>
<td align="left"><p>创建由系统测试根密钥或其他指定的密钥签名的 x.509 证书。</p>
<p>WDK 文档：</p>
<p><a href="makecert.md" data-raw-source="[&lt;strong&gt;MakeCert&lt;/strong&gt;](makecert.md)"><strong>MakeCert</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>MSBuild （Msbuild.exe）</p>
<p><strong>WDK 工具：</strong>不</p></td>
<td align="left"><p>随 Visual Studio 一起安装</p></td>
<td align="left"><p>生成 Microsoft WDK 中提供的示例、驱动程序和关联的软件组件。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=262804" data-raw-source="[MSBuild]( https://go.microsoft.com/fwlink/p/?linkid=262804)">MSBuild</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>PnpCpu （PnPCpu）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\PnPCpu.exe</p>
<p>%WindowsSdkDir%\tools\x86\PnPCpu.exe</p></td>
<td align="left"><p>模拟热添加处理器到正在运行的 Windows Server 2008 实例。</p>
<p>WDK 文档：</p>
<p><a href="pnpcpu.md" data-raw-source="[PNPCPU](pnpcpu.md)">PNPCPU</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>PnPUtil （PnPUtil）</p>
<p><strong>WDK 工具：</strong>不</p></td>
<td align="left"><p>%Windir%\system32\pnputil.exe</p></td>
<td align="left"><p>一种命令行工具，可用于安装或删除 Windows 驱动程序存储区中的<a href="https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages" data-raw-source="[driver packages](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)">驱动程序包</a>。</p>
<p>Windows 7 和更高版本的 Windows 中提供了此工具。</p>
<p>WDK 文档：</p>
<p><a href="pnputil.md" data-raw-source="[PnPUtil](pnputil.md)">PnPUtil</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>PoolMon （Poolmon）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\poolmon.exe</p>
<p>%WindowsSdkDir%\tools\x86\poolmon.exe</p></td>
<td align="left"><p>显示操作系统从系统的分页和非分页内核池收集内存分配的数据，以及用于终端服务会话的内存池。 数据按池分配标记进行分组。</p>
<p>WDK 文档：</p>
<p><a href="poolmon.md" data-raw-source="[PoolMon](poolmon.md)">PoolMon</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>PowerCfg （PowerCfg）</p>
<p><strong>WDK 工具：</strong>不</p></td>
<td align="left"><p>%Windir%\system32\powercfg.exe</p></td>
<td align="left"><p>用于评估系统能效的命令行工具。</p>
<p>Windows 7 和更高版本的 Windows 中提供了此工具。</p>
<p>开发人员中心文档：</p>
<a href="https://download.microsoft.com/download/7/E/7/7E7662CF-CBEA-470B-A97E-CE7CE0D98DC2/PowerCfg.docx" data-raw-source="[Using PowerCfg to Evaluate System Energy Efficiency](https://download.microsoft.com/download/7/E/7/7E7662CF-CBEA-470B-A97E-CE7CE0D98DC2/PowerCfg.docx)">使用 PowerCfg 评估系统能效</a>
<p>有关命令选项的信息，请键入</p>
<p></p>
<p><strong>PowerCfg/？</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Pvk2Pfx （Pvk2Pfx）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\Pvk2Pfx.exe</p>
<p>%WindowsSdkDir%\bin\x86\Pvk2Pfx.exe</p></td>
<td align="left"><p>将 .spc、.cer 和 pvk 文件中包含的公钥和私钥信息复制到个人信息交换（.pfx）文件。</p>
<p>WDK 文档：</p>
<p><a href="pvk2pfx.md" data-raw-source="[&lt;strong&gt;Pvk2Pfx&lt;/strong&gt;](pvk2pfx.md)"><strong>Pvk2Pfx</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>PwrTest （Pwrtest）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\pwrtest.exe</p>
<p>%WindowsSdkDir%\tools\x86\pwrtest.exe</p></td>
<td align="left"><p>适用于 Windows 7 和更高版本的电源管理工具，用于在计算机上执行和记录电源管理信息。</p>
<p>WDK 文档：</p>
<p><a href="pwrtest.md" data-raw-source="[PwrTest](pwrtest.md)">PwrTest</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>SignTool （SignTool）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\SignTool.exe</p>
<p>%WindowsSdkDir%\bin\x86\SignTool.exe</p></td>
<td align="left"><p>对文件进行数字签名，验证文件和时间戳文件中的签名。</p>
<p>WDK 文档：</p>
<p><a href="signtool.md" data-raw-source="[&lt;strong&gt;SignTool&lt;/strong&gt;](signtool.md)"><strong>SignTool</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Stampinf （Stampinf）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\stampinf.exe</p>
<p>%WindowsSdkDir%\bin\x86\stampinf.exe</p></td>
<td align="left"><p>更新常见 INF 文件指令，包括<strong>DriverVer</strong>指令。</p>
<p>WDK 文档：</p>
<p><a href="stampinf.md" data-raw-source="[Stampinf](stampinf.md)">Stampinf</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>静态驱动程序验证程序</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\SDV</p>
<p></p>
<div class="alert">
<strong>请注意</strong>  从 Visual Studio 中的 "<strong>驱动程序</strong>" 菜单启动 "静态驱动程序验证程序"。
</div>
<div>
 
</div></td>
<td align="left"><p>用于驱动程序的静态验证工具，可系统地分析 Windows 驱动程序的源代码，并确定驱动程序是否与 Windows 操作系统内核正确交互。</p>
<p>WDK 文档：</p>
<p><a href="static-driver-verifier.md" data-raw-source="[Static Driver Verifier](static-driver-verifier.md)">静态驱动程序验证程序</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Tracefmt （Tracefmt）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\tracefmt.exe</p>
<p>%WindowsSdkDir%\bin\x86\tracefmt.exe</p></td>
<td align="left"><p>格式化并显示事件跟踪日志文件（.etl）或实时跟踪会话中的跟踪消息。</p>
<p>WDK 文档：</p>
<p><a href="tracefmt.md" data-raw-source="[Tracefmt](tracefmt.md)">Tracefmt</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>TraceLog （Tracelog）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p><strong>WDK 8：</strong></p>
<p>%WindowsSdkDir%\tools\x64\tracelog.exe</p>
<p>%WindowsSdkDir%\tools\x86\tracelog.exe</p>
<p><strong>WDK 8.1：</strong></p>
<p>%WindowsSdkDir%\bin\x64\tracelog.exe</p>
<p>%WindowsSdkDir%\bin\x86\tracelog.exe</p>
<p>%WindowsSdkDir%\bin\arm\tracelog.exe</p></td>
<td align="left"><p>从命令行配置和控制跟踪会话。 度量延迟的过程调用（Dpc）和中断服务例程（Isr）所用的时间。</p>
<p>WDK 文档：</p>
<p><a href="tracelog.md" data-raw-source="[Tracelog](tracelog.md)">Tracelog</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>TracePDB （Tracepdb）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\tracepdb.exe</p>
<p>%WindowsSdkDir%\bin\x86\tracepdb.exe</p></td>
<td align="left"><p>使用 WPP 跟踪提供程序的完整或专用 PDB 符号文件创建跟踪消息格式（tmf）文件。</p>
<p>WDK 文档：</p>
<p><a href="tracepdb.md" data-raw-source="[Tracepdb](tracepdb.md)">Tracepdb</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>TraceView （Traceview）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\TraceView.exe</p>
<p>%WindowsSdkDir%\tools\x86\TraceView.exe</p></td>
<td align="left"><p>配置和控制跟踪会话，并显示实时跟踪会话和跟踪日志中的格式化跟踪消息。 TraceView 具有一个图形用户界面和一个用于批处理和脚本编写的命令行接口。</p>
<p>WDK 文档：</p>
<p><a href="traceview.md" data-raw-source="[TraceView](traceview.md)">TraceView</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>TraceWPP （Tracewpp）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\tracewpp.exe</p>
<p>%WindowsSdkDir%\bin\x86\tracewpp.exe</p></td>
<td align="left"><p>运行 Windows 软件跟踪预处理器（WPP）。</p>
<p>WDK 文档：</p>
<p><a href="wpp-preprocessor.md" data-raw-source="[WPP Preprocessor](wpp-preprocessor.md)">WPP 预处理器</a></p>
<p><a href="survey-of-software-tracing-tools.md" data-raw-source="[Survey of Software Tracing Tools](survey-of-software-tracing-tools.md)">软件跟踪工具的调查</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>WDF 测试器</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64&lt;/p&gt;
<p>%WindowsSdkDir%\tools\x86&lt;/p&gt;</td>
<td align="left"><p>一组可用于测试、验证和调试 WDF 驱动程序的工具。 工具集提供可在脚本或已编译的应用程序中使用的 WMI 编程接口。</p>
<p>WDK 文档：</p>
<p><a href="wdftester--wdf-driver-testing-toolset.md" data-raw-source="[WdfTester: WDF Driver Testing Toolset](wdftester--wdf-driver-testing-toolset.md)">WdfTester： WDF 驱动程序测试工具集</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WDF 验证程序（您尚未 wdfverifier）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\wdfverifier.exe</p>
<p>%WindowsSdkDir%\tools\x86\wdfverifier.exe</p></td>
<td align="left"><p>为 KMDF 和 UMDF 驱动程序的框架验证程序提供了一个易于使用的界面。</p>
<p>WDK 文档：</p>
<p><a href="wdf-verifier-control-application.md" data-raw-source="[WDF Verifier Control Application](wdf-verifier-control-application.md)">WDF 验证程序控件应用程序</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>设备上的 Web 服务（WSD）基本互操作性工具（WSDBIT）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p><strong>WSDBIT 客户端：</strong></p>
<p>%WindowsSdkDir%\tools\x64\ wsdbit_client .exe</p>
<p>%WindowsSdkDir%\tools\x86\ wsdbit_client .exe</p>
<p><strong>WSDBIT 服务器：</strong></p>
<p>%WindowsSdkDir%\tools\x64\ wsdbit_server .exe</p>
<p>%WindowsSdkDir%\tools\x86\ wsdbit_server .exe</p></td>
<td align="left"><p>验证<a href="https://go.microsoft.com/fwlink/p/?linkid=81255" data-raw-source="[Device Profile for Web Services (DPWS)](https://go.microsoft.com/fwlink/p/?linkid=81255)">Web 服务（DPWS）的设备配置文件</a>实现是否适用于 WSDAPI。</p>
<p>WDK 文档：</p>
<p><a href="wsdapi-basic-interoperability-tool.md" data-raw-source="[WSD Interoperability Tool](wsdapi-basic-interoperability-tool.md)">WSD 互操作性工具</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Winerror.h （Winerror.h）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\winerror.exe</p>
<p>%WindowsSdkDir%\tools\x86\winerror.exe</p></td>
<td align="left"><p>返回指定错误（Winerror.h）或成功代码（Ntstatus .h）的错误消息标识符和映射信息。</p>
<p>有关命令选项的信息，请键入</p>
<p><strong>winerror.h/？</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>WMIMofCk （Wmimofck）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x86\wmimofck.exe</p></td>
<td align="left"><p>WDK 文档：</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/using-wmimofck-exe" data-raw-source="[Using wmimofck.exe](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-wmimofck-exe)">使用 wmimofck</a></p>
<p>有关命令选项的信息，请键入</p>
<p><strong>wmimofck -?</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>WsdCodeGen （Wsdcodegen）</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\wsdcodegen.exe</p>
<p>%WindowsSdkDir%\bin\x86\wsdcodegen.exe</p></td>
<td align="left"><p>基于 Web 服务协定自动生成代理和存根。 您可以使用此工具来创建客户端应用程序。 不过，你可以使用它来测试或创建用户模式驱动程序。</p>
<p>验证二进制 MOF 文件（. bmf）中指定的类、属性、方法和事件对于 WMI 使用是否有效。 生成 MOF 支持文件。</p>
<p>Windows SDK：</p>
<p>请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=81407" data-raw-source="[Web Services on Devices](https://go.microsoft.com/fwlink/p/?linkid=81407)">Web 服务设备</a>部分</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WSDDebug_client 和 WSDDebug_host</p>
<p><strong>WDK 工具：</strong>是的</p></td>
<td align="left"><p><strong>调试客户端：</strong></p>
<p>%WindowsSdkDir%\bin\x64\ WSDDebug_client .exe</p>
<p>%WindowsSdkDir%\bin\x86\ WSDDebug_client .exe</p>
<p><strong>调试主机：</strong></p>
<p>%WindowsSdkDir%\bin\x64\ WSDDebug_host .exe</p>
<p>%WindowsSdkDir%\bin\x86\ WSDDebug_host .exe</p></td>
<td align="left"><p>这些工具是可以用来对设备或应用程序进行故障排除的软设备和客户端。</p>
<p>Windows SDK：</p>
<p>请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=81407" data-raw-source="[Web Services on Devices](https://go.microsoft.com/fwlink/p/?linkid=81407)">Web 服务设备</a>部分</p></td>
</tr>
</tbody>
</table>

 

### WDK 中用于 Windows 8.1 的新增功能<a name="what-s-new-in-the-wdk-for-windows8-1"></a>

已在 WDK 8.1 中添加或更改以下工具：

-   HCK 测试套件（请参阅[如何使用 Visual Studio 在运行时测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)以及[如何在 WDK 8.1 中运行 HCK 测试套件](https://docs.microsoft.com/windows-hardware/drivers)。）

-   [驱动程序验证程序](driver-verifier.md)—现在有四个用于检测 Windows 驱动程序中的错误的新选项。
-   [PwrTest](pwrtest.md)—更新的文档、新的测试方案，包括对连接待机电源状态的支持。
-   [Tracelog](tracelog.md)—新选项。

### Windows 8 的 WDK 新增功能<a name="what-s-new-in-the-wdk-for-windows8"></a>

以下工具已添加到适用于 Windows 8 的 WDK：

-   蓝牙查询记录验证程序（Sdpverify）

-   设备基础测试（请参阅[如何使用 Visual Studio 在运行时测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)以及[如何选择和配置设备基础测试](https://docs.microsoft.com/windows-hardware/drivers)。

-   传感器诊断工具（sensordiagnostictool）

### 适用于 Windows 8 的 WDK 中发生了哪些更改<a name="what-s-changed-in-the-wdk-for-windows8"></a>
以下工具位于适用于 Windows 7 的 Microsoft WDK 中，但在 Windows 8 的 WDK 中未包含。

-   Windows Biometric Framework 工具（BioTest、WBDIDriverTest）

-   设备路径试验（devpathexer）。 现在，设备基本模糊测试的一部分。

-   IoSpy 和 IoAttack （IoSpyCmd，IoAttack）。 现在是设备基础测试的一部分。

-   不再支持 Kernrate （Kernrate） Kernrate。 而是使用[Windows 性能分析工具包](https://go.microsoft.com/fwlink/p/?linkid=294280)。

-   Microsoft 自动代码审核（OACR）（驱动程序组件现在是 Visual Studio 中的代码分析工具的一部分。）

-   即插即用驱动程序测试（pnpdtest）。 现在是设备基础测试的一部分。

-   ProCalc

-   WWAN 驱动程序测试应用（wwandrivertestapp）

### <a name="supported-platforms"></a>支持的平台

WDK 8.1 支持开发在这些版本的 Windows 上运行的驱动程序：

-   Windows 8.1 和 Windows 8

-   Windows Server 2012 R2 和 Windows Server 2012

-   Windows 7

-   Windows Server 2008 R2

-   对于 Windows Vista （包括 SP1 和 SP2），必须使用 WDK 8。 对于 Windows XP，必须使用 WDK 7。

你可以在这些版本的 Windows 上运行集成的 Visual Studio 驱动程序开发环境。

-   Windows 8.1 和 Windows 8

-   Windows Server 2012 R2 和 Windows Server 2012

-   Windows 7

-   Windows Server 2008 R2

 

 

