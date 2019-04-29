---
title: 静态驱动程序验证程序诊断
description: 静态驱动程序验证程序诊断
ms.assetid: dff22144-43a0-427f-8075-9c9152670933
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffe5655e2916d59eca26b695e569aeeadc22a85f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382970"
---
# <a name="static-driver-verifier-diagnostics"></a>静态驱动程序验证程序诊断


SDV 具有一种诊断模式，可帮助你和 Microsoft 对 SDV 可能遇到的问题进行故障排除。 启用诊断模式，SDV 消息记录到一系列的驱动程序项目，其中一个每个阶段的验证和每个规则中的文件。

### <a name="span-idenablingdiagnosticsspanspan-idenablingdiagnosticsspanenabling-diagnostics"></a><span id="enabling_diagnostics"></span><span id="ENABLING_DIAGNOSTICS"></span>启用诊断

从命令行运行时才可启用当前 SDV （也称为调试模式） 可用于诊断模式。  从命令行运行的详细信息，请参阅[Static Driver Verifier 命令 (MSBuild)](-static-driver-verifier-commands--msbuild-.md)。

若要激活诊断，请添加 **/debug**标志后 **/check**命令。  例如：

```
msbuild /t:sdv /p:Inputs="/check:* /debug" mydriver.VcxProj /p:Configuration="Release" /p:Platform=x64
```

启用诊断程序将导致显著更多输出到命令窗口中，以及特定日志文件的创建。

### <a name="span-idenablingdiagnosticsspanspan-idenablingdiagnosticsspanunderstanding-diagonistics"></a><span id="enabling_diagnostics"></span><span id="ENABLING_DIAGNOSTICS"></span>了解 Diagonistics

每个阶段的执行，这将提供有关该步骤的详细信息，SDV 将创建多个文件。  SDV 失败时仅执行过程，它将为后续阶段中创建任何 diagonistic 文件。

创建的文件的顺序：
* **smvexecute-NormalBuild.log**:这位于您的驱动程序源目录中，并显示 SDV 的初始尝试生成而无需其他检测和分析驱动程序的输出。
* **smvexecute InterceptedBuild.log**:这位于您的驱动程序源目录中，并显示 SDV 生成分析挂钩添加驱动程序的输出。  
* **smvcl.log**:这位于驱动程序项目中创建的 SDV"sdv"目录中。  它显示了 InterceptedBuild 步骤的编译器输出。  如果你看到的故障**smvexecute InterceptedBuild.log**，你可能能够找到更多详细信息中的**smvcl.log。**

* **smvexecute Scan.log**:这位于驱动程序项目中创建的 SDV"sdv"目录中。  它显示了 SDV 的尝试扫描以查找入口点的驱动程序的输出。  此处的错误可能表示不找到的任何入口点，并应更新你的函数 roletypes 或 sdv map.h。  请参阅[使用函数角色类型声明](using-function-role-type-declarations.md)并[批准 Sdv map.h 文件](approving-the-sdv-map-h-file.md)有关详细信息。
* **smvexecute FinalCompile.log**:这些文件之一为每个规则验证的 sdv，并可在创建"sdv\check\[规则名称]"驱动程序项目中的 SDV 创建的子文件夹。  此文件显示 SDV 的尝试生成包含 OS 模型和特定规则驱动程序的输出。  
* **smvexecute-CheckRule.log**:这些文件之一为每个规则验证的 sdv，并可在创建"sdv\check\[规则名称]"驱动程序项目中的 SDV 创建的子文件夹。  此文件显示 SDV 的尝试验证指定的规则对您的驱动程序的输出。

您应查找的列出为命令输出中失败的阶段相对应的文件。  如果发生了故障**FinalCompile**或**CheckRule**步骤，确保检查文件夹中的特定规则列为失败。
