---
title: 静态驱动程序验证程序输入文件
description: 静态驱动程序验证程序输入文件
keywords:
- 静态驱动程序验证程序 WDK，输入文件
- StaticDV WDK，输入文件
- SDV WDK，输入文件
- 输入文件 WDK 静态驱动程序验证程序
- 文件 WDK 静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d6654275d3c6d7e9b10e2da10a649eabcac7e6e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799745"
---
# <a name="static-driver-verifier-input-files"></a>静态驱动程序验证程序输入文件


SDV [验证引擎](verification-engine.md) 使用以下文件作为验证的输入。 所有验证只需要驱动程序源文件和操作系统模型文件。

-   驱动程序项目文件和源代码。 在项目文件所在的目录中运行 SDV。

-   [操作系统模型文件](operating-system-model.md)。 SDV 根据你为验证选择的规则选择并组装操作系统模型文件。

-   [处理的库文件](library-processing-in-static-driver-verifier.md)。 仅当驱动程序依赖于非系统库时才需要库文件。 有关信息和说明，请参阅静态驱动程序验证程序中的库处理。

-   [规则列表文件](static-driver-verifier-rule-list-file.md)。 请参阅 [静态驱动程序验证程序命令 (MSBuild) ](-static-driver-verifier-commands--msbuild-.md)。

-   [静态驱动程序验证程序选项文件](static-driver-verifier-options-file.md)。 SDV 创建一个全局选项文件，其中包含适用于所有 SDV 验证的设置。 若要为驱动程序创建本地选项文件，请复制全局选项文件。 然后，可以编辑全局选项文件的副本，以创建驱动程序的本地选项文件。

评估 SDV 验证的结果时，务必检查输入文件，确认验证中使用的所有输入文件的准确性和完整性。

本部分包括以下文件的详细说明：

[静态驱动程序验证程序规则列表文件](static-driver-verifier-rule-list-file.md)

[静态驱动程序验证程序选项文件](static-driver-verifier-options-file.md)

 

 





