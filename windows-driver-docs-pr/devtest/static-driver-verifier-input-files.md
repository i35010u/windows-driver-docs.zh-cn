---
title: 静态驱动程序验证程序输入文件
description: 静态驱动程序验证程序输入文件
ms.assetid: 0c31a752-6946-4704-aff6-c9cd1bf9f522
keywords:
- 静态驱动程序验证程序 WDK，输入文件
- StaticDV WDK 输入文件
- SDV WDK 输入文件
- 输入文件 WDK Static Driver Verifier
- 文件 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d79e38c64ac7365e4cc9e562ba07d93d00dd0e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353465"
---
# <a name="static-driver-verifier-input-files"></a>静态驱动程序验证程序输入文件


SDV[验证引擎](verification-engine.md)将以下文件作为输入验证。 驱动程序源文件和操作系统模型文件所需的所有验证。

-   驱动程序项目文件和源代码。 项目文件所在的目录中运行 SDV。

-   [操作系统模型文件](operating-system-model.md)。 SDV 选择，并组装操作系统模型文件根据您选择用于验证的规则。

-   [处理库文件](library-processing-in-static-driver-verifier.md)。 仅当该驱动程序依赖于非系统库时，才需要使用库文件。 有关信息和说明，请参阅库中 Static Driver Verifier 的处理。

-   [规则列表文件](static-driver-verifier-rule-list-file.md)。 请参阅[Static Driver Verifier 命令 (MSBuild)](-static-driver-verifier-commands--msbuild-.md)。

-   [Static Driver Verifier 选项文件](static-driver-verifier-options-file.md)。 SDV 创建包含适用于所有 SDV 验证后设置的全局选项文件。 若要创建一个驱动程序的本地选项文件，将复制的全局选项文件。 然后可以编辑全局选项文件以创建该驱动程序的本地选项文件的副本。

评估时的 SDV 验证结果，它是非常重要，检查输入的文件，以确认的准确性和完整性验证中使用的所有输入文件。

本部分包括以下文件的详细的说明：

[Static Driver Verifier 规则列表文件](static-driver-verifier-rule-list-file.md)

[Static Driver Verifier 选项文件](static-driver-verifier-options-file.md)

 

 





