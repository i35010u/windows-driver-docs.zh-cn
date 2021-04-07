---
title: 创建驱动程序验证日志
description: 了解为什么 Windows Server 硬件认证计划需要所有适用的驱动程序在提交时提供驱动程序验证日志 (DVL)。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 960b24b096d6ad4362bab9155483e0aa7fe0ffbc
ms.sourcegitcommit: ed3ba7c8d91a5a4de6f8ef46097eb992e94ba609
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "106087175"
---
# <a name="creating-a-driver-verification-log"></a>创建驱动程序验证日志

[Windows 硬件认证计划](/windows-hardware/design/compatibility/)的某些计划要求对各项驱动程序提交提供驱动程序验证日志 (DVL)。 DVL 包含来自代码分析 (CA)、静态驱动程序验证程序 (SDV) 和 [CodeQL](../devtest/static-tools-and-codeql.md) 日志文件的结果的摘要。 DVL 不包含任何源信息。 在为驱动程序创建 DVL 之前，必须先运行代码分析工具和静态驱动程序验证程序。

**如何创建驱动程序验证日志**

1.  在运行代码分析工具之前，请确保可以使用最新 Windows 驱动程序工具包 (WDK) 生成并链接驱动程序。
2.  对于驱动程序解决方案，请确保已选择版本配置作为解决方案配置，并选择 x64 作为解决方案平台。
3.  运行[静态驱动程序验证程序](../devtest/static-driver-verifier.md)。 有关创建日志文件中的信息，请参阅[为静态驱动程序验证程序创建日志文件](creating-a-log-file-for-static-driver-verifier.md)和[使用静态驱动程序验证程序查找驱动程序中的缺陷](../devtest/using-static-driver-verifier-to-find-defects-in-drivers.md)。
4.  为驱动程序运行代码分析工具。 解决并修复发现的任何缺陷。 请参阅[为代码分析工具创建日志文件](creating-a-log-file-for-the-code-analysis-tool.md)和[如何为驱动程序运行代码分析](../devtest/how-to-run-code-analysis-for-drivers.md)。 有关代码分析的详细信息，请参阅[使用代码分析分析 C/C++ 代码质量](/previous-versions/visualstudio/visual-studio-2013/dd264897(v=vs.120))。
5.  运行 CodeQL。  解决并修复发现的缺陷。  如果未更正被视为“必须修复”的缺陷，则认证将失败。  有关 CodeQL 和静态工具徽标测试的详细信息，请参阅 [CodeQL 和静态工具徽标测试](../devtest/static-tools-and-codeql.md)。
5.  创建驱动程序验证日志。 在“驱动程序”菜单中，选择“创建驱动程序验证日志…”。
6.  确认检测到代码分析日志、静态驱动程序验证程序日志和 CodeQL 日志文件。 选择“创建”。

驱动程序验证日志的文件扩展名为 .DVL.XML。 日志在项目文件夹中创建，例如，\\*myDriverProject*\\*myDriverName*.DVL.XML。

**注意**  SDV 对驱动程序执行彻底的重新生成操作，这会删除代码分析日志。  因此，请务必在运行 CA 之前运行 SDV。

**注意** 在准备好使用 [Windows Hardware Lab Kit](/windows-hardware/test/hlk/) 测试驱动程序时，需要将驱动程序验证日志复制到测试计算机上的 %systemdrive%\\DVL 目录下。 在复制新驱动程序验证日志之前，请确保删除测试计算机上该目录中的内容。

 
## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注

有关代码分析工具、静态驱动程序验证程序和驱动程序验证日志的最新信息，请参阅“WDK 发行说明”。 发行说明可在 [Windows 驱动程序工具包 (WDK) 下载页](https://go.microsoft.com/fwlink/p/?linkid=254897)上找到。

**重要提示** 认证提交可接受 DVL 文件出现超时、加宽行距和其他未成功结果。 这不会导致 HLK 中的静态工具测试失败。 
 
还可以从“Visual Studio 命令提示”窗口创建驱动程序验证日志，不管是使用与 Visual Studio 一起安装的 Visual Studio 本机工具命令提示符，还是使用企业 Windows 驱动程序工具包 (EWDK)：

```cpp
msbuild.exe <vcxprojectfile> /target:dvl /p:Configuration="Release" /P:Platform=x64
```

## <a name="creating-a-driver-verification-log-outside-of-msbuild-or-visual-studio"></a>在 msbuild 或 Visual Studio 外部创建驱动程序验证日志

Microsoft 随附 [Windows 驱动程序工具包 (WDK)](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk) 和 [Enterprise WDK (eWDK)](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk#enterprise-wdk-ewdk-for-windows-10-version-2004) 提供一种名为 dvl.exe 的组件，它可用于通过命令行生成驱动程序验证日志 (DVL)。  从 WDK/eWDK 预览版 21342 及更高版本开始，可在 msbuild 或 Visual Studio 上下文之外通过命令行生成 DVL。 按照以下步骤通过命令行创建 DVL：

1. 将创建 DVL 所需的结果置于单个目录中。  通常，对于旨在针对 Windows 客户端进行认证的驱动程序，这是 [CodeQL SARIF 文件](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-tools-and-codeql#view-analysis)。  对于 Windows Server 认证，这还可能包含代码分析和静态驱动程序验证程序 (SDV) 结果文件。  请查看 [WHCP 要求](https://docs.microsoft.com/windows-hardware/design/compatibility/whcp-specifications-policies)文档，具体详细了解需要运行哪些工具来进行设备驱动程序认证。
2. 应将 CodeQL SARIF 文件和代码分析 XML 文件置于目录的顶层。  应将 SDV DVL.xml 文件置于“sdv”子文件夹中。
3. 在命令行中，导航到包含 CodeQL SARIF 文件的顶层目录。
4. 从 WDK 或装载的 eWDK 中查找 dvl.exe。
5. 通过传递 /manualCreate 标志、驱动程序名称和所需的体系结构来调用 dvl.exe。 例如：

```cmd
"C:\Program Files (x86)\Windows Kits\10\Tools\dvl\dvl.exe" /manualCreate driverName driverArchitecture
```

应对 driverArchitecture 字符串使用以下字符串之一：

- X86
- X64
- ARM
- ARM64

**不要在 driverName 字符串中包含“.sys”**

6. 检查生成的 DVL 以确保它生成无误

此用法主要用于生成带有 CodeQL 结果的 DVL，但也可用于 SDV 和 CA 结果。  

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题



* [为静态驱动程序验证程序创建日志文件](creating-a-log-file-for-static-driver-verifier.md)
* [为代码分析工具创建日志文件](creating-a-log-file-for-the-code-analysis-tool.md)
* [硬件认证计划](/previous-versions/windows/hardware/hck/jj124227(v=vs.85))
* [使用代码分析工具分析驱动程序质量](analyzing-driver-quality-by-using-code-analysis-tools.md)
* [如何为驱动程序运行“代码分析”](../devtest/how-to-run-code-analysis-for-drivers.md)
* [使用静态驱动程序验证程序查找驱动程序中的缺陷](../devtest/using-static-driver-verifier-to-find-defects-in-drivers.md)
* [CodeQL 和静态工具徽标测试](../devtest/static-tools-and-codeql.md)