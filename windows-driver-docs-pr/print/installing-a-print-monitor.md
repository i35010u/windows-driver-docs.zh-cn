---
title: 安装打印监视器
description: 安装打印监视器
ms.assetid: 2ab993fd-647b-40aa-981c-1bc270ec79a4
keywords:
- 打印监视器 WDK，安装
- 安装打印监视器 WDK
- INF 文件，WDK 打印，打印监视器
- 语言监视器 WDK 打印，安装
- 端口监视 WDK 打印，安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 317655db61b6cddc3ed449733c202686c1ef522c
ms.sourcegitcommit: d9a9925f790271f4ca2c8377d551d96e8d1e62c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88850226"
---
# <a name="installing-a-print-monitor"></a>安装打印监视器





本部分介绍可用于安装打印监视器的方法。  (可以使用安装打印机所用的同一 INF 文件来安装打印监视器。 有关 INF 文件的详细信息，请参阅 [即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-plug-and-play) 和 [电源管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-power-management)。 ) 

### <a name="installing-a-language-monitor"></a><a href="" id="ddk-installing-a-language-monitor-gg"></a>安装语言监视器

若要安装语言监视器，请将 LanguageMonitor 条目添加到 INF 文件的 [**Inf DDInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section) 。 在 LanguageMonitor 项中，列出语言监视器的显示名称及其 DLL 的名称，类似于以下 INF 示例。 必须为每个打印机驱动程序包含一个 LanguageMonitor 条目，以便控制需要使用语言监视器的打印机。 有关详细信息，请参阅 [打印机 INF 文件](printer-inf-files.md)。

```cpp
[AcmeInst]
CopyFiles=@ACME.PPD,ACMEMON
DataSection=PSCRIPT_DATA
DataFile=ACME.PPD
LanguageMonitor="Acme Language Monitor,acmemon.dll"
Include=ntprint.inf
Needs=PSCRIPT.OEM

[ACMEMON]
acmemon.dll,,,0x00000020

[DestinationDirs]
DefaultDestDir=66000
ACMEMON=66002

[SourceDisksNames]
1= %Location%,,,

[SourceDisksFiles]
acme.ppd = 1,\i386
acmemon.dll = 1,\i386
```

添加驱动程序向导或添加打印机向导将读取此 INF 文件并安装与打印机驱动程序关联的语言监视器。

或者，自定义安装应用程序可以通过调用后台处理程序的 **AddMonitor** 函数来安装语言监视器，以显式仅安装特定的监视器 DLL。

Microsoft Windows SDK 文档中介绍了 (**AddMonitor** 函数。 ) 

### <a name="installing-a-port-monitor"></a><a href="" id="ddk-installing-a-port-monitor-gg"></a>安装端口监视器

若要安装端口监视器，你的安装介质必须包含一个打印机 INF 文件 (即，该类 = 打印机) 包含 PortMonitors 部分的 INF 文件。 此部分中的单个条目指向包含两个条目的 "安装" 部分：一个 [**INF CopyFiles 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive) ，该指令列出组成端口监视器的所有文件，一个 PortMonitorDll 项用于指定上列表中的哪个 DLL 实现端口监视器接口。 下面的示例代码演示了这些要点。 PortMonitors 部分指向名为 SamplePortMon 的安装部分。 在该部分中，INF **CopyFiles** 指令复制三个文件组成端口监视器。 之后，PortMonitorDll 条目会标识实现端口监视器接口的 DLL。

```cpp
[PortMonitors]
"Sample Port Monitor" = SamplePortMon

[SamplePortMon]
CopyFiles = @file1.dll, @file2.dll, @file3.hlp
PortMonitorDll = file1.dll
```

若要安装端口监视器，请在 "控制面板" 中打开 "打印机" 文件夹。 在 "打印机" 文件夹的 " **文件** " 菜单上，选择 " **服务器属性**"。 在 " **文件服务器属性** " 对话框中，单击 " **端口** " 选项卡，然后单击 " **添加端口 ...** " 按钮。 在 " **打印机端口** " 对话框中，单击 " **新端口类型 ...** " 按钮。 在文本输入框中键入 INF 文件的路径，然后单击 **"确定"**。

或者，自定义安装应用程序可以通过调用 **AddMonitor** 函数来安装端口监视器 DLL，如 [端口监视器](https://docs.microsoft.com/windows/desktop/printdocs/port-monitors)中所述。

 

 




