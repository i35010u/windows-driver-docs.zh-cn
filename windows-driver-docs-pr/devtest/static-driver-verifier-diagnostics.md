---
title: 静态驱动程序验证程序诊断
description: 静态驱动程序验证程序诊断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99e5c21766331418bc77eb08b67d4b6da534e50a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828811"
---
# <a name="static-driver-verifier-diagnostics"></a>静态驱动程序验证程序诊断


SDV 提供诊断模式，可帮助你和 Microsoft 解决 SDV 可能会遇到的问题。 启用诊断模式后，SDV 会将消息记录到驱动程序项目中的一系列文件，每个验证阶段和每个规则一个。

### <a name="span-idenabling_diagnosticsspanspan-idenabling_diagnosticsspanenabling-diagnostics"></a><span id="enabling_diagnostics"></span><span id="ENABLING_DIAGNOSTICS"></span>启用诊断

在从命令行运行时，当前仅可启用 SDV 的诊断模式 (也称为调试模式) 。  有关从命令行运行的详细信息，请参阅 [静态驱动程序验证程序命令 (MSBuild) ](-static-driver-verifier-commands--msbuild-.md)。

若要激活诊断，请在 **/check** 命令后添加 **/debug** 标志。  例如：

```
msbuild /t:sdv /p:Inputs="/check:* /debug" mydriver.VcxProj /p:Configuration="Release" /p:Platform=x64
```

启用诊断将导致更多的输出到 "命令" 窗口，以及创建特定的日志文件。

### <a name="span-idenabling_diagnosticsspanspan-idenabling_diagnosticsspanunderstanding-diagonistics"></a><span id="enabling_diagnostics"></span><span id="ENABLING_DIAGNOSTICS"></span>了解未

SDV 将在执行的每个阶段创建多个文件，这些文件将提供有关此步骤的详细信息。  当 SDV 在时发生执行失败时，不会创建任何 diagonistic 文件以供以后使用。

创建的文件顺序如下：
* **smvexecute-NormalBuild**：此项位于驱动程序的源目录中，并显示 SDV 的初始尝试生成驱动程序的输出，而无需进行其他检测和分析。
* **smvexecute-InterceptedBuild**：此项位于驱动程序的源目录中，并显示 SDV 生成驱动程序的输出，并添加分析挂接。  
* **smvcl**：这位于通过 sdv 在驱动程序项目中创建的 "sdv" 目录中。  它显示 InterceptedBuild 步骤的编译器输出。  如果 **smvexecute-InterceptedBuild** 中出现故障，则可以在 smvcl 中找到更多详细信息 **。**

* **smvexecute-Scan**：这位于通过 sdv 在驱动程序项目中创建的 "sdv" 目录中。  它显示 SDV 尝试扫描驱动程序以查找入口点的输出。  此处的错误可能表示找不到入口点，应更新函数 roletypes 或 sdv。  有关详细信息，请参阅 [使用函数角色类型声明](using-function-role-type-declarations.md) 和 [批准 Sdv 文件](approving-the-sdv-map-h-file.md) 。
* **smvexecute-FinalCompile**：为 sdv 验证的每个规则创建这些文件中的一个，可以在 \[ 驱动程序项目 sdv 创建的 "sdv\check rule name]" 子文件夹中找到。  此文件显示 SDV 的输出，其中包含操作系统型号和特定规则生成驱动程序的尝试。  
* **smvexecute-CheckRule**：为 sdv 验证的每个规则创建这些文件中的一个，可以在 \[ 驱动程序项目 sdv 创建的 "sdv\check rule name]" 子文件夹中找到。  此文件显示 SDV 尝试根据你的驱动程序验证指定规则的输出。

应在命令输出中查找对应于暂存列表的文件。  如果 **FinalCompile** 或 **CheckRule** 步骤中发生失败，请务必检查文件夹中是否列出了作为失败的特定规则。
