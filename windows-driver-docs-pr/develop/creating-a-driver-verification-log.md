---
ms.assetid: 5EB802D0-1894-4D64-ACB0-77B848B7E644
title: 创建驱动程序验证日志
description: Windows Server 2012 硬件认证计划需要所有驱动程序在正当提交时提供驱动程序验证日志 (DVL)。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 630db8890a4710b71178e3357bffa819bd4cc902
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "77575203"
---
# <a name="creating-a-driver-verification-log"></a>创建驱动程序验证日志

Windows Server [硬件认证计划](https://docs.microsoft.com/windows-hardware/design/compatibility/)需要所有驱动程序在正当提交时提供驱动程序验证日志 (DVL)。 DVL 包含代码分析 (CA) 的结果和静态驱动程序验证程序 (SDV) 日志文件的摘要。 DVL 不包含任何源信息。 在为驱动程序创建 DVL 之前，必须先运行代码分析工具和静态驱动程序验证程序。

**如何创建驱动程序验证日志**

1.  在运行代码分析工具之前，请确保可以使用最新 Windows 驱动程序工具包 (WDK) 生成并链接驱动程序。
2.  对于驱动程序解决方案，请确保已选择版本配置作为解决方案配置，并选择 x64 作为解决方案平台。
3.  运行[静态驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)。 有关创建日志文件中的信息，请参阅[为静态驱动程序验证程序创建日志文件](creating-a-log-file-for-static-driver-verifier.md)和[使用静态驱动程序验证程序查找驱动程序中的缺陷](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)。
4.  为驱动程序运行代码分析工具。 解决并修复发现的任何缺陷。 请参阅[为代码分析工具创建日志文件](creating-a-log-file-for-the-code-analysis-tool.md)和[如何为驱动程序运行代码分析](https://docs.microsoft.com/windows-hardware/drivers/devtest/how-to-run-code-analysis-for-drivers)。 有关代码分析的详细信息，请参阅[使用代码分析分析 C/C++ 代码质量](https://go.microsoft.com/fwlink/p/?linkid=226836)。
5.  创建驱动程序验证日志。 在“驱动程序”  菜单中，单击“创建驱动程序验证日志…”  。
6.  确认检测到代码分析日志和静态驱动程序验证程序日志文件。 单击“**创建**”。

驱动程序验证日志的文件扩展名为 .DVL.XML。 日志在项目文件夹中创建，例如，\\*myDriverProject*\\*myDriverName*.DVL.XML。

**注意**  SDV 对驱动程序执行彻底的重新生成操作，这会删除代码分析日志。  因此，请务必在运行 CA 之前运行 SDV。

**注意**  在准备好使用 [Windows Hardware Lab Kit](https://docs.microsoft.com/windows-hardware/test/hlk/) 测试驱动程序时，需要将驱动程序验证日志复制到测试计算机上的 %systemdrive%\\DVL 目录下。 在复制新驱动程序验证日志之前，请确保删除测试计算机上该目录中的内容。

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


有关代码分析工具、静态驱动程序验证程序和驱动程序验证日志的最新信息，请参阅“WDK 发行说明”。 发行说明可在 [Windows 驱动程序工具包 (WDK) 下载页](https://go.microsoft.com/fwlink/p/?linkid=254897)上找到。

**重要提示**  认证提交可以接受 DVL 文件出现超时、加宽行距和其他未成功结果。 这不会导致 HCK 中的静态工具测试失败。 对于 HCK 2.0，静态工具测试只需要 DVL 文件存在，就可证明已运行代码分析和 SDV，并不需要通过所有规则。

 

还可以从“Visual Studio 命令提示”窗口创建驱动程序验证日志，不管是使用与 Visual Studio 一起安装的 Visual Studio 本机工具命令提示符，还是使用企业 Windows 驱动程序工具包 (EWDK)：

```cpp
msbuild.exe <vcxprojectfile> /target:dvl /p:Configuration="Release" /P:Platform=x64
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [为静态驱动程序验证程序创建日志文件](creating-a-log-file-for-static-driver-verifier.md)
* [为代码分析工具创建日志文件](creating-a-log-file-for-the-code-analysis-tool.md)
* [硬件认证计划](https://go.microsoft.com/fwlink/p/?linkid=227016)
* [使用代码分析工具分析驱动程序质量](analyzing-driver-quality-by-using-code-analysis-tools.md)
* [如何为驱动程序运行“代码分析”](https://docs.microsoft.com/windows-hardware/drivers/devtest/how-to-run-code-analysis-for-drivers)
* [使用静态驱动程序验证程序查找驱动程序中的缺陷](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)
 

 






