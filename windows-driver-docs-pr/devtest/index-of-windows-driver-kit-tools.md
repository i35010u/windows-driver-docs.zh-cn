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
- GUIDGen.exe WDK
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2cad3aadc999fbe590f15ed34446a23d3e271da4
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382677"
---
# <a name="index-of-windows-driver-kit-tools"></a>Windows 驱动程序工具包工具的索引

本主题提供有关 Windows 驱动程序工具包 (WDK) 中包含的工具的基本信息。 本主题还包括对驱动程序开发有用的其他工具的参考。 这些其他工具要么作为操作系统的一部分提供，要么作为单独的下载提供。 有关每个工具的详细信息，请参阅本主题介绍该工具的文档。

有关如何获取最新 WDK 的信息，请参阅 [下载 Windows 驱动程序工具包 (WDK) ](../download-the-wdk.md)。

## <a name="index-of-wdk-tools"></a>WDK 工具的索引

下表中的信息描述了适用于 Windows 驱动程序开发人员的工具。 工具列表包括由 wdk **工具** 字段) 提供的随 (wdk 提供的工具，还包括一些单独提供或随 Windows 一起安装的工具。 [所有](#all-drivers)驱动程序通常都列出可用于所有驱动程序的工具。 特定于技术的工具组合在一起，例如，特定于 [Windows 便携设备的工具 (WPD) 驱动程序](#windows-portable-devices-wpd-drivers) 或 [传感器](#sensors)。

- [音频/视频驱动程序](#audio--video-drivers)
- [蓝牙驱动程序](#bluetooth-drivers)
- [Windows 映像获取 (WIA) 驱动程序](#windows-image-acquisition-wia-drivers)
- [ (WPD) 驱动程序的 Windows 便携式设备](#windows-portable-devices-wpd-drivers)
- [打印机驱动程序](#printer-drivers)
- [传感器](#sensors)
- [所有驱动程序](#all-drivers)

>[!NOTE]
>Visual Studio 环境变量% WindowsSdkDir% 表示安装此 WDK 版本的 Windows 工具包目录的路径，例如，C： \\ Program Files (x86) \\ Windows 工具包 \\ 8.1。

### <a name="audio--video-drivers"></a>音频/视频驱动程序

|工具名称|工具位置|说明和帮助文件位置|
|----|----|----|
|显示颜色校准工具 ( # A0)  </br>**WDK 工具**：否|% Windir% \System32\Dccw.exe</br>|一种校准工具，它使用户能够调整其显示颜色，使其更接近 Windows 和万维网国际标准红绿蓝 (sRGB) 颜色空间。|
|GraphEdt ( # A0) </br>**WDK 中的工具：** 是的|% WindowsSdkDir% \tools\x86\graphedt.exe</br>% WindowsSdkDir% \tools\x64\graphedt.exe|生成筛选器关系图以测试流式传输音频/视频捕获驱动程序。</br>文档：</br>[GraphEdit 概述](/windows/win32/directshow/simulating-graph-building-with-graphedit)|
|KSStudio ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x86\KsStudio.exe</br> % WindowsSdkDir% \tools\x64\KsStudio.exe</br></br>**注意** 此工具必须由具有管理员权限的用户运行。|此工具可以构造筛选器图的图形表示形式，该图显示了筛选器与筛选器的内部节点之间的 pin 到针连接。</br>%WindowsSdkDir%\tools\x86\KsStudio.chm</br>%WindowsSdkDir%\tools\x64\KsStudio.chm</br>有关详细信息，请参阅 [AVStream 测试和调试](../stream/avstream-testing-and-debugging.md) 。|
|USB 设备查看器 ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x86\Usbview.exe</br>% WindowsSdkDir% \tools\x64\Usbview.exe|枚举 USB 主机控制器、USB 集线器和连接的 USB 设备，并可以从注册表查询设备信息，并通过 USB 请求将设备查询到设备。</br>可以从代码库中获取 USB 设备查看器的源代码，请参阅 [USBVIEW 示例应用程序](/samples/microsoft/windows-driver-samples/usbview-sample-application/)|

### <a name="bluetooth-drivers"></a>蓝牙驱动程序

|工具名称|工具位置|说明和帮助文件位置|
|----|----|----|
|蓝牙查询记录验证器 ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x86\Sdpverifiy.exe</br>% WindowsSdkDir% \tools\x64\Sdpverifiy.exe|显示 Windows 解释蓝牙设备的查询记录。</br>WDK 文档：[蓝牙查询记录验证](bluetooth-inquiry-record-verifier.md)程序|

### <a name="windows-image-acquisition-wia-drivers"></a>Windows 映像获取 (WIA) 驱动程序

|工具名称|工具位置|说明和帮助文件位置|
|----|----|----|
|WIADbgCfg ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x86\wiadbgcfg.exe</br>% WindowsSdkDir% \tools\x64\wiadbgcfg.exe|为 WIA 驱动程序启用日志记录 (Windows Server 2008 和更高版本的 Windows) 。</br>**注意** 对于早期版本的 Windows，请使用 WIALogCfg。</br>% WindowsSdkDir% \tools\x86\wiadbgcfg.htm</br>% WindowsSdkDir% \tools\x64\wiadbgcfg.htm|
|WIAInfo2 ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x86\wiainfo2.exe</br>% WindowsSdkDir% \tools\x64\wiainfo2.exe|显示 WIA 项树，以便您可以查看和编辑 WIA 设备驱动程序属性。</br>% WindowsSdkDir% \tools\x86\wiainfo2.htm</br>% WindowsSdkDir% \tools\x64\wiainfo2.htm|
|WIAPreview ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\wiapreview.exe</br>% WindowsSdkDir% \tools\x86\wiapreview.exe|演示如何使用 WIA 预览组件和驱动程序的分段筛选器。</br>% WindowsSdkDir% \tools\x64\wiapreview.htm</br>% WindowsSdkDir% \tools\x86\wiapreview.htm|
|WIATest ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\wiatest.exe</br>% WindowsSdkDir% \tools\x86\wiatest.exe|显示由驱动程序所公开的驱动程序、Windows 图像获取 (WIA) 的属性的项树以及每个属性的当前值。 您可以使用此工具在开发和单元测试过程中调试驱动程序。</br>% WindowsSdkDir% \tools\x64\wiatest.htm</br>% WindowsSdkDir% \tools\x64\wiatest.htm|
|Windows 映像跟踪文件查看器 ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\Wiatrcvw.exe</br>% WindowsSdkDir% \tools\x86\Wiatrcvw.exe|显示 WIA 跟踪日志 (%WINDIR%\Debug\WIA\wiatrace.log) ，并使你可以更改每个模块的 WIA 跟踪参数。</br>%WindowsSdkDir%\tools\x64\Wiatrcvw.mht</br>%WindowsSdkDir%\tools\x64\Wiatrcvw.mht|

### <a name="windows-portable-devices-wpd-drivers"></a> (WPD) 驱动程序的 Windows 便携式设备

|工具名称|工具位置|说明和帮助文件位置|
|----|----|----|
|WpdDeviceInspector ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\WpdDeviceInspector.exe</br>% WindowsSdkDir% \tools\x86\WpdDeviceInspector.exe|查询 WPD 驱动程序，并生成全面的 HTML 报告，用于描述设备及其功能。 例如，你可以使用它来检索受支持的设备命令和对象的列表。 此工具将生成每个对象支持的所有属性的列表。</br>WDK 文档：</br>[Windows 便携设备](/windows/win32/windows-portable-devices)</br>[WPD 驱动程序开发工具](../portable/familiarizing-yourself-with-the-sample-driver.md)|
|WpdInfo ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\WpdInfo.exe</br>% WindowsSdkDir% \tools\x86\WpdInfo.exe|执行常见的 WPD 操作，例如：打开和关闭设备、在设备上创建或删除对象以及发出设备命令。</br>WDK 文档：</br>[Windows 便携设备](/windows/win32/windows-portable-devices)</br>[WPD 驱动程序开发工具](../portable/familiarizing-yourself-with-the-sample-driver.md)|
|Microsoft 网络监视器 ( # A0) </br>**WDK 工具：** 不|下载 Microsoft 网络监视器</br>[NetMon.exe](https://www.microsoft.com/download/details.aspx?displaylang=en&id=4865)|显示 WPD 组件中的跟踪信息。 此工具取代了以前版本的 WDK 附带的 WpdMon.exe。</br>WDK 文档：</br>[Windows 便携设备](/windows/win32/windows-portable-devices)</br>[WPD 驱动程序开发工具](../portable/familiarizing-yourself-with-the-sample-driver.md)，请参阅 [使用网络监视器工具](../portable/using-the-netmon-tool.md)。|

### <a name="printer-drivers"></a>打印机驱动程序

|工具名称|工具位置|说明和帮助文件位置|
|----|----|----|
|GPDCheck ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\gpdcheck.exe</br>% WindowsSdkDir% \tools\x86\gpdcheck.exe|验证一般打印机说明文件 (GPD) 的语法正确性。</br>有关命令选项的信息，请键入 </br>**gpdcheck /?**|
|INFGate ( # A0) </br>**WDK 工具：** 是的|WindowsSdkDir% \tools\x64\infgate.exe</br>% WindowsSdkDir% \tools\x86\infgate.exe.exe|验证打印机 INF 文件的一致性。</br>有关命令选项的信息，请键入</br>**infgate /?**|
|Isxps.exe ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\isxps\isxps.exe</br>% WindowsSdkDir% \tools\x86\isxps\isxps.exe|验证 XPS 文件与 XPS 和 OPC 规范的符合性。</br>有关命令选项的信息，请键入</br>**isxps.exe/？** 在命令提示符窗口中。</br>有关详细信息，请参阅 [Isxps.exe 一致性工具](/previous-versions/aa348104(v=vs.110))|
|Looksgood ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\looksgood.exe</br>% WindowsSdkDir% \tools\x86\looksgood.exe|验证 XPS 呈现引擎的正确性。</br>有关命令选项的信息，请键入</br>**looksgood /?**|
|MakeNTF ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\makentf.exe</br>% WindowsSdkDir% \tools\x86\makentf.exe|将) 文件和东亚字体 AFM 文件 (AFM 字体度量转换为 Windows 字体文件 ( contoso.ntf) 。</br>WDK 文档：</br>[将 AFM 文件转换为 NTF 文件](../print/converting-afm-files-to-ntf-files.md)</br>[将东亚版 AFM 文件转换为 NTF 文件](../print/converting-east-asian-afm-files-to-ntf-files.md)|
|PPDCheck ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\ppdcheck.exe</br>% WindowsSdkDir% \tools\x86\ppdcheck.exe|验证 PostScript 打印机说明文件 (PPD) 的语法正确性。</br>有关命令选项的信息，请键入</br>**ppdcheck /?**|
|PTConform ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\PTConform.exe</br>% WindowsSdkDir% \tools\x86\PTConform.exe|验证打印票证或打印功能文档是否符合打印架构。</br>有关命令选项的信息，请键入</br>**ptconform /?**|
|XpsAnalyzer ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\XpsAnalyzer.exe</br>% WindowsSdkDir% \tools\x86\XpsAnalyzer.exe|分析 XML 纸张规范 (XPS) 文件，以与 XPS 1.0 规范兼容。</br>WDK 文档：</br>[XpsAnalyzer](xpsanalyzer.md)|

### <a name="sensors"></a>传感器

|工具名称|工具位置|说明和帮助文件位置|
|----|----|----|
|传感器诊断工具 ( # A0) </br>**WDK 工具：** 是的|%WindowsSdkDir%\tools\x64</br>%WindowsSdkDir%\tools\x86|测试传感器和位置功能的驱动程序、固件和硬件。 该工具调用传感器和位置 API 来测试数据检索、事件处理、报告间隔、更改敏感度、属性检索。</br>WDK 文档：</br>[通过传感器诊断工具测试传感器功能](../sensors/the-sensor-diagnostic-tool.md)|

### <a name="all-drivers"></a>所有驱动程序

|工具名称|工具位置|说明和帮助文件位置|
|----|----|----|
|BinPlace ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \bin\x86\binplace.exe|通过移动文件、从可执行文件提取符号以及从符号文件中删除私有符号，管理大型编码项目。</br>WDK 文档：</br>[BinPlace](binplace.md)|
|驱动程序的代码分析</br>**WDK 工具：** 是的|代码分析工具包含在 Visual Studio 中。 安装 WDK 时，会添加驱动程序特定的组件。|检测 C 和 c + + 编码错误的静态验证工具。 此版本专用于检测内核模式驱动程序中的错误。</br>WDK 文档：</br>[驱动程序的代码分析](code-analysis-for-drivers.md)|
|Certmgr.msc ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \bin\x64\CertMgr.exe</br>% WindowsSdkDir% \bin\x86\CertMgr.exe|管理证书、证书信任列表 (Ctl) 和证书吊销列表 (Crl) 用于签署驱动程序和 [驱动程序包](../install/driver-packages.md)。</br>WDK 文档：</br>[CertMgr](certmgr.md)|
|ChkINF</br>**WDK 工具：** 弃用|先前路径：</br>%WindowsSdkDir%\tools\x86\Chkinf|ChkInf 已被弃用。 相反，请使用 [InfVerif](infverif.md)。</br>WDK 文档：</br>[InfVerif](infverif.md)|
|计算机硬件标识工具 ( # A0) </br>**WDK 工具：** 是的|**Windows 驱动程序工具包 (WDK) 8：**</br>% WindowsSdkDir% \tools\x64\ComputerHardwareIds.exe</br>% WindowsSdkDir% \tools\x86\ComputerHardwareIds.exe</br>WDKPath\tools\Other\ia64\ComputerHardwareIds.exe</br>**Windows 驱动程序工具包 (WDK) 8.1：**</br>% WindowsSdkDir% \bin\x64\ComputerHardwareIds.exe</br>% WindowsSdkDir% \bin\x86\ComputerHardwareIds.exe</br>% WindowsSdkDir% \bin\arm\ComputerHardwareIds.exe|从 SMBIOS 信息派生计算机硬件 Id。</br>WDK 文档：</br>[ComputerHardwareIds](computerhardwareids.md)|
|DC2WMIParser ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\DC2WMIParser.exe</br>% WindowsSdkDir% \tools\x86\DC2WMIParser.exe|DC2WMIParser 是一种工具，用于收集驱动程序验证器创建的 WMI IRP 记录，并将此日志转换为文本文件。</br>文档：</br>[IRP 日志记录](./irp-logging.md)|
|依赖关系查看 ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\depends.exe</br>% WindowsSdkDir% \tools\x86\depends.exe|显示树关系图中应用程序所需的模块的依赖关系模式。 显示内容包括很多详细信息，包括每个模块导出的函数、其他模块实际调用的函数和加载和运行模块所需的最小文件集。</br>在该工具中，从 **依赖关系** 查看 "帮助" 菜单中选择 " **帮助主题**"。|
|DevCon ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\devcon.exe</br>% WindowsSdkDir% \tools\x86\devcon.exe|设备管理器的命令行版本。 DevCon 启用、禁用、安装、配置和删除本地计算机上的设备，并显示有关本地和远程计算机上的设备的详细信息。</br>WDK 文档：</br>[DevCon](devcon.md)|
|驱动程序 ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\drivers.exe</br>% WindowsSdkDir% \tools\x86\drivers.exe|显示计算机上安装的所有驱动程序的列表。</br>WDK 文档：</br>无|
|驱动程序验证程序 ( # A0) </br>**WDK 工具：** 不|% Windir% \system32\verifier.exe|监视内核模式驱动程序和图形驱动程序，以检测可能损坏系统的非法函数调用或操作。 它可以将驱动程序用于各种强调和测试，以找出不正确的行为。</br>WDK 文档：</br>[驱动程序验证程序](driver-verifier.md)|
|驱动程序验证日志 (DVL) </br>**WDK 工具：** 是的|需要 Microsoft Visual Studio 和 WDK。 从 "**驱动程序**" 菜单中，选择 "**创建驱动程序验证日志 ...** "。|[静态工具徽标测试](/windows-hardware/test/hlk/testref/6ab6df93-423c-4af6-ad48-8ea1049155ae)需要驱动程序验证日志 (DVL) 用于所有适用的驱动程序提交。 DVL 包含代码分析的结果和静态驱动程序验证程序日志文件的摘要。 请参阅 [创建驱动程序验证日志](../develop/creating-a-driver-verification-log.md)。|
|增强的存储证书管理工具 ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\ehstorcertmgrcmd.exe</br>% WindowsSdkDir% \tools\x86\ehstorcertmgrcmd.exe|管理兼容 IEEE 1667 标准的 USB 存储设备上的证书。</br>WDK 文档：</br>[增强的存储证书管理工具](enhanced-storage-certificate-management-tool.md)|
|事件和性能计数器清单生成器工具 ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \bin\x64\ECManGen.exe</br>% WindowsSdkDir% \bin\x86\ECManGen.exe|用于创建事件或性能计数器清单 ( *) 的工具，无需使用 XML 标记即可从头开始。 有关创建清单文件的信息，请参阅将 [检测清单写入 (Windows) ](/windows/desktop/WES/writing-an-instrumentation-manifest) 部分和向 [内核模式驱动程序添加事件跟踪](adding-event-tracing-to-kernel-mode-drivers.md)|
|Inf2Cat ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \bin\x64\inf2cat.exe</br>% WindowsSdkDir% \bin\x86\inf2cat.exe|确定是否可以为指定的 Windows 版本列表对 [驱动程序包的](../install/driver-packages.md) INF 文件进行数字签名，如果是，则将生成适用于指定 windows 版本的未签名的 [目录文件](../install/catalog-files.md) 。</br>WDK 文档：</br>[Inf2Cat](inf2cat.md)|
|InfVerif ( # A0) </br>**WDK 工具：** 是的|c:\Program 文件 (x86) \Windows Kits\10\tools\arm\infverif.exe</br>c:\Program 文件 (x86) \Windows Kits\10\tools\arm64\infverif.exe</br>c:\Program 文件 (x86) \Windows Kits\10\tools\x86\infverif.exe</br>c:\Program 文件 (x86) \Windows Kits\10\tools\x64\infverif.exe|测试驱动程序 INF 文件。 除了报告 INF 语法问题外，该工具还报告 INF 文件是否是通用的。</br>WDK 文档：</br>[InfVerif](infverif.md)|
|MakeCat ( # A0) </br>**WDK 工具：** 是的|WDKPath\bin\amd64\MakeCat.exe</br>WDKPath\bin\ia64\MakeCat.exe</br>WDKPath\bin\x86\MakeCat.exe|为[驱动程序包](../install/driver-packages.md)创建[编录文件](../install/catalog-files.md)。</br>WDK 文档：</br>[MakeCat](makecat.md)|
|MakeCert ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \bin\x64\MakeCert.exe</br>% WindowsSdkDir% \bin\x86\MakeCert.exe|创建由系统测试根密钥或其他指定的密钥签名的 x.509 证书。</br>WDK 文档：</br>[MakeCert](makecert.md)|
|MSBuild ( # A0) /br>**WDK 工具：** 否|随 Visual Studio 一起安装|生成 Microsoft WDK 中提供的示例、驱动程序和关联的软件组件。</br>[MSBuild]( /visualstudio/msbuild/msbuild?view=vs-2015)|
|PnpCpu ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\PnPCpu.exe</br>% WindowsSdkDir% \tools\x86\PnPCpu.exe|模拟热添加处理器到正在运行的 Windows Server 2008 实例。</br>WDK 文档：</br>[PNPCPU](pnpcpu.md)|
|PnPUtil ( # A0) </br>**WDK 工具：** 不|% Windir% \system32\pnputil.exe|一种命令行工具，可用于安装或删除 Windows 驱动程序存储区中的 [驱动程序包](../install/driver-packages.md) 。</br>WDK 文档：</br>[PnPUtil](pnputil.md)|
|PoolMon ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\poolmon.exe</br>% WindowsSdkDir% \tools\x86\poolmon.exe|显示操作系统从系统的分页和非分页内核池收集内存分配的数据，以及用于终端服务会话的内存池。 数据按池分配标记进行分组。</br>WDK 文档：</br>[PoolMon](poolmon.md)|
|PowerCfg ( # A0) </br>**WDK 工具：** 不|% Windir% \system32\powercfg.exe|用于评估系统能效的命令行工具。</br>开发人员中心文档：</br>[使用 PowerCfg 评估系统能效](https://download.microsoft.com/download/7/E/7/7E7662CF-CBEA-470B-A97E-CE7CE0D98DC2/PowerCfg.docx)</br>有关命令选项的信息，请键入</br>**PowerCfg/？**|
|Pvk2Pfx ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \bin\x64\Pvk2Pfx.exe</br>% WindowsSdkDir% \bin\x86\Pvk2Pfx.exe|将 .spc、.cer 和 pvk 文件中包含的公钥和私钥信息复制到个人信息交换 ( .pfx) 文件中。</br>WDK 文档：</br>[Pvk2Pfx](pvk2pfx.md)|
|PwrTest ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\pwrtest.exe</br>% WindowsSdkDir% \tools\x86\pwrtest.exe|一种电源管理工具，用于在计算机上练习和记录电源管理信息。</br>WDK 文档：</br>[PwrTest](pwrtest.md)|
|SignTool ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \bin\x64\SignTool.exe</br>% WindowsSdkDir% \bin\x86\SignTool.exe|对文件进行数字签名，验证文件和时间戳文件中的签名。</br>WDK 文档：</br>[SignTool](signtool.md)|
|Stampinf ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \bin\x64\stampinf.exe</br>% WindowsSdkDir% \bin\x86\stampinf.exe|更新常见 INF 文件指令，包括 **DriverVer** 指令。</br>WDK 文档：</br>[Stampinf](stampinf.md)|
|静态驱动程序验证程序</br>**WDK 工具：** 是的|%WindowsSdkDir%\tools\SDV</br></br>**注意**  从 Visual Studio 中的 " **驱动程序** " 菜单启动 "静态驱动程序验证程序"。|用于驱动程序的静态验证工具，可系统地分析 Windows 驱动程序的源代码，并确定驱动程序是否与 Windows 操作系统内核正确交互。</br>WDK 文档：</br>[静态驱动程序验证程序](static-driver-verifier.md)|
|Tracefmt ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \bin\x64\tracefmt.exe</br>% WindowsSdkDir% \bin\x86\tracefmt.exe|格式化并显示事件跟踪日志文件 ( .etl) 或实时跟踪会话中的跟踪消息。</br>WDK 文档：</br>[Tracefmt](tracefmt.md)|
|TraceLog ( # A0) </br>**WDK 工具：** 是的|**WDK 8：**</br>% WindowsSdkDir% \tools\x64\tracelog.exe</br>% WindowsSdkDir% \tools\x86\tracelog.exe</br>**WDK 8.1：**</br>% WindowsSdkDir% \bin\x64\tracelog.exe</br>% WindowsSdkDir% \bin\x86\tracelog.exe</br>% WindowsSdkDir% \bin\arm\tracelog.exe|从命令行配置和控制跟踪会话。 度量延迟过程调用所用的时间 (Dpc) 和中断服务例程 (Isr) 。</br>WDK 文档：</br>[Tracelog](tracelog.md)|
|TracePDB ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \bin\x64\tracepdb.exe</br>% WindowsSdkDir% \bin\x86\tracepdb.exe|从 WPP 跟踪提供程序的完整或专用 PDB 符号文件中 () 文件创建跟踪消息格式。</br>WDK 文档：</br>[Tracepdb](tracepdb.md)|
|TraceView ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\TraceView.exe</br>% WindowsSdkDir% \tools\x86\TraceView.exe|配置和控制跟踪会话，并显示实时跟踪会话和跟踪日志中的格式化跟踪消息。 TraceView 具有一个图形用户界面和一个用于批处理和脚本编写的命令行接口。</br>WDK 文档：</br>[TraceView](traceview.md)|
|TraceWPP ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \bin\x64\tracewpp.exe</br>% WindowsSdkDir% \bin\x86\tracewpp.exe|运行 Windows 软件跟踪预处理器 (WPP) 。</br>WDK 文档：</br>[WPP 预处理器](wpp-preprocessor.md)</br>[软件跟踪工具调查](survey-of-software-tracing-tools.md)|
|WDF 测试器</br>**WDK 工具：** 是的|%WindowsSdkDir%\tools\x64</br>%WindowsSdkDir%\tools\x86|一组可用于测试、验证和调试 WDF 驱动程序的工具。 工具集提供可在脚本或已编译的应用程序中使用的 WMI 编程接口。</br>WDK 文档：</br>[WdfTester：WDF 驱动程序测试工具集](wdftester--wdf-driver-testing-toolset.md)|
|WDF 验证器 ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\wdfverifier.exe</br>% WindowsSdkDir% \tools\x86\wdfverifier.exe|为 KMDF 和 UMDF 驱动程序的框架验证程序提供了一个易于使用的界面。</br>WDK 文档：</br>[WDF 验证程序控制应用程序](wdf-verifier-control-application.md)|
|设备上的 Web 服务 (WSD) 基本互操作性工具 (WSDBIT) </br>**WDK 工具：** 是的|**WSDBIT 客户端：**</br>% WindowsSdkDir% \tools\x64\wsdbit_client.exe</br>% WindowsSdkDir% \tools\x86\wsdbit_client.exe</br>**WSDBIT 服务器：**</br>% WindowsSdkDir% \tools\x64\wsdbit_server.exe</br>% WindowsSdkDir% \tools\x86\wsdbit_server.exe|验证 Web 服务的设备配置文件的实现 (DPWS) 使用 WSDAPI。</br>WDK 文档：</br>[WSD 互操作性工具](wsdapi-basic-interoperability-tool.md)|
|Winerror.h ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \tools\x64\winerror.exe</br>% WindowsSdkDir% \tools\x86\winerror.exe|返回 (Winerror.h) 的指定错误的错误消息标识符和映射信息， (Ntstatus) 返回成功代码。</br>有关命令选项的信息，请键入</br>**winerror.h/？**|
|WMIMofCk ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \bin\x86\wmimofck.exe|WDK 文档：</br>[使用 wmimofck.exe](../kernel/using-wmimofck-exe.md)</br>有关命令选项的信息，请键入</br>**wmimofck -?**|
|WsdCodeGen ( # A0) </br>**WDK 工具：** 是的|% WindowsSdkDir% \bin\x64\wsdcodegen.exe</br>% WindowsSdkDir% \bin\x86\wsdcodegen.exe|基于 Web 服务协定自动生成代理和存根。 您可以使用此工具来创建客户端应用程序。 不过，你可以使用它来测试或创建用户模式驱动程序。</br>验证在二进制 MOF 文件 () 中指定的类、属性、方法和事件对于 WMI 使用是否有效。 生成 MOF 支持文件。</br>Windows SDK：</br>请参阅 [Web 服务设备](/windows/win32/wsdapi/wsd-portal) 部分|
|WSDDebug_client 和 WSDDebug_host</br>**WDK 工具：** 是的|**调试客户端：**</br>% WindowsSdkDir% \bin\x64\WSDDebug_client.exe</br>% WindowsSdkDir% \bin\x86\WSDDebug_client.exe</br>**调试主机：**</br>% WindowsSdkDir% \bin\x64\WSDDebug_host.exe</br>
% WindowsSdkDir% \bin\x86\WSDDebug_host.exe|这些工具是可以用来对设备或应用程序进行故障排除的软设备和客户端。</br>Windows SDK：</br>["在设备上 Web 服务"](/windows/win32/wsdapi/wsd-portal) 部分|

### <a name="supported-platforms"></a>支持的平台

你可以在 Windows 7 和更高版本上运行 Windows 10 WDK，并使用它来开发这些操作系统的驱动程序：

运行时要求

|客户端 OS|服务器 OS|
|----|----|
|Windows 10|Windows Server 2019、Windows Server 2016|
|Windows 8.1|Windows Server 2012 R2|
|Windows 8|Windows Server 2012|
|Windows 7|Windows Server 2008 R2 SP1|