---
ms.assetid: 4985B206-9E7F-45FE-9067-7CFD15A7AAAD
title: 为代码分析工具创建日志文件
description: Windows Server 2012 硬件认证计划需要所有驱动程序在正当提交时提供驱动程序验证日志 (DVL)。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 111695456dc09cb05daef55a6f4b1ddde232207f
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734455"
---
# <a name="creating-a-log-file-for-the-code-analysis-tool"></a>为代码分析工具创建日志文件

Windows Server 2012 [硬件认证计划](/previous-versions/windows/hardware/hck/jj124227(v=vs.85))需要所有驱动程序在正当提交时提供驱动程序验证日志 (DVL)。 在为驱动程序创建 DVL 之前，你必须先运行代码分析工具。 DVL 包含代码分析的结果和静态驱动程序验证程序日志文件的摘要。 日志文件不包含源代码信息。

**对驱动程序运行代码分析**

1.  在 Microsoft Visual Studio Ultimate 2012 中，选择驱动程序项目文件，然后选择并按住（或右键单击）打开项目属性。 选择“Windows 8 版本”  作为“配置”  ，并选择“x64”  作为“平台”  。
2.  从“分析”或“生成”菜单中，选择“对解决方案运行 Code Analysis”。
3.  如果发现错误或警告，请使用“代码分析报告”  窗口调查错误产生的原因。 使用警告消息解决这些问题。 有关代码分析工具的详细信息，请参阅[如何为驱动程序运行代码分析](../devtest/how-to-run-code-analysis-for-drivers.md)和[使用“代码分析”分析 C/C++ 代码质量](/previous-versions/visualstudio/visual-studio-2013/dd264897(v=vs.120))。

驱动程序的代码分析工具会将结果写入项目的生成配置和平台子目录中的文件 vc.nativecodeanalysis.all.xml，例如，\\Windows 8Release\\x64。

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


驱动程序的代码分析是编译时使用的静态验证工具，它检测 C 和 C++ 程序中的基本编码错误，并包括专门检测（主要）内核模式驱动程序代码中的错误的专用模块。 在 WDK 的以前版本中，代码分析的驱动程序特定模块是称为 PREfast for Drivers (PFD) 的独立工具的一部分。

你还可以从“Visual Studio 命令提示”窗口运行代码分析工具。 通过运行以下批处理文件之一设置环境。

```cpp
"C:\Program Files\Microsoft Visual Studio 11.0\VC\vcvarsall.bat" x64
```

-或者-

```cpp
"C:\Program Files (x86)\Microsoft Visual Studio 11.0\VC\vcvarsall.bat" x64
```

运行代码分析工具。

```cpp
msbuild.exe <vcxprojectfile> /p:Configuration="Win8 Release" /P:Platform=x64 /target:clean
msbuild.exe <vcxprojectfile> /p:Configuration="Win8 Release" /P:Platform=x64 /P:RunCodeAnalysisOnce=True
```

有关驱动程序验证日志的要求的最新信息，请参阅“WDK 发行说明”。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [创建驱动程序验证日志](creating-a-driver-verification-log.md)
* [为静态驱动程序验证程序创建日志文件](creating-a-log-file-for-static-driver-verifier.md)
* [驱动程序的代码分析](../devtest/code-analysis-for-drivers.md)
* [硬件认证计划](/previous-versions/windows/hardware/hck/jj124227(v=vs.85))
* [使用“代码分析”分析 C/C++ 代码质量](/previous-versions/visualstudio/visual-studio-2013/dd264897(v=vs.120))
* [如何为驱动程序运行“代码分析”](../devtest/how-to-run-code-analysis-for-drivers.md)
