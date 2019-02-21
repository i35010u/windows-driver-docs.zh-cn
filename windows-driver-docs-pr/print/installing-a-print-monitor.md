---
title: 安装打印监视器
description: 安装打印监视器
ms.assetid: 2ab993fd-647b-40aa-981c-1bc270ec79a4
keywords:
- 打印监视器 WDK，安装
- 安装 WDK 的打印监视器
- INF 文件 WDK 打印、 打印监视器
- 打印语言监视器 WDK 安装
- 端口监视器 WDK 打印，安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a984a8e558b4c77cf82a905911a9b0bb07183e70
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519430"
---
# <a name="installing-a-print-monitor"></a>安装打印监视器





本部分介绍的方法可以用来安装打印监视器。 （你可以使用相同的 INF 文件用于安装您的打印机安装打印监视器。 有关 INF 文件的详细信息，请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)并[电源管理](https://msdn.microsoft.com/library/windows/hardware/ff547131)。)

### <a href="" id="ddk-installing-a-language-monitor-gg"></a>安装语言监视器

若要安装的语言监视器，LanguageMonitor 将条目添加到[ **INF DDInstall 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)的 INF 文件。 LanguageMonitor 条目中列出的语言监视器的显示的名称和其 DLL，类似于下面的示例 INF 的名称。 LanguageMonitor 条目必须包含的每个控件无需使用的语言监视器打印机的打印机驱动程序。 有关详细信息，请参阅[打印机 INF 文件](printer-inf-files.md)。

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

添加驱动程序向导或添加打印机向导读取此 INF 文件并安装打印机驱动程序与关联的语言监视器。

或者，自定义安装应用程序可以通过调用后台处理程序的安装语言监视器**AddMonitor**函数，以显式安装仅在特定监视器 DLL。

( **AddMonitor**函数 Microsoft Windows SDK 文档中所述。)

### <a href="" id="ddk-installing-a-port-monitor-gg"></a>安装端口监视器

若要安装端口监视器，安装介质必须包括打印机 INF 文件 (即，哪个类的 INF 文件 = 打印机)，其中包含 PortMonitors 部分。 本部分中的单个条目指向安装部分，其中包含两个条目： [ **INF CopyFiles 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546346) ，它列出的所有文件端口监视器和 PortMonitorDll 条目组成，在上一列表实现中指定的端口监视器接口的 DLL。 下面的代码示例说明了这些点。 PortMonitors 部分指向名为 SamplePortMon 安装部分。 在该部分中，INF **CopyFiles**指令将复制构成端口监视器的三个文件。 接下来，PortMonitorDll 条目标识实现端口监视器界面的 DLL。

```cpp
[PortMonitors]
"Sample Port Monitor" = SamplePortMon

[SamplePortMon]
CopyFiles = @file1.dll, @file2.dll, @file3.hlp
PortMonitorDll = file1.dll
```

若要安装端口监视器，请在控制面板中打开打印机文件夹。 在打印机文件夹**文件**菜单中，选择**服务器属性**。 上**文件服务器属性**对话框中，单击**端口**选项卡，然后依次**添加端口...** 按钮。 上**打印机端口**对话框中，单击**新建端口类型...** 按钮。 在文本输入框中，键入 INF 文件的路径，然后单击**确定**。

或者，自定义安装应用程序可以安装端口通过调用监视 DLL **AddMonitor**函数中所述[端口监视器](https://msdn.microsoft.com/library/windows/desktop/dd162825.aspx)。

 

 




