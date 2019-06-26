---
title: 验证过程
description: 验证过程
ms.assetid: 3803771b-94ef-4e02-9d08-8703283b3f99
keywords:
- 静态驱动程序验证程序 WDK，验证过程
- StaticDV WDK，验证过程
- SDV WDK，验证过程
- 验证过程 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23dd1149e2fd1a7d47a2b47b6c039760e64994ad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381797"
---
# <a name="verification-process"></a>验证过程


SDV 开展*验证*，也就是说，一个测试，以确定是否该驱动程序的实际行为符合规则，用于定义正确的行为。

当您提交的命令以验证驱动程序时，SDV 执行三步骤过程中，在此期间它将确定哪些文件，它需要、 准备文件，并验证该驱动程序。

本主题介绍在每个验证过程的步骤中会发生什么情况。

### <a name="span-idbuildspanspan-idbuildspanbuild"></a><span id="build"></span><span id="BUILD"></span>生成

期间**生成**步骤中，SDV 编译链接，并生成使用 MSBuild 的驱动程序。

### <a name="span-idscanspanspan-idscanspanscan"></a><span id="scan"></span><span id="SCAN"></span>扫描

期间**扫描**步骤中，SDV 扫描函数角色类型声明的驱动程序的代码、 组装驱动程序入口点的列表，创建[Sdv map.h](sdv-map-h.md)存储目录中的文件*源*的驱动程序文件 (称为**驱动程序的源目录**)。

### <a name="span-idcheckspanspan-idcheckspancheck"></a><span id="check"></span><span id="CHECK"></span>Check

期间**检查**步骤中，SDV 准备要进行和用于验证使用所选的规则来验证该驱动程序。 可以选择的规则的详细信息，请参阅[驱动程序验证程序的静态规则](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

SDV 开始通过确定如果所选的规则要求的操作系统模型的其他组件。 如果是这样，SDV 将其他操作系统模型文件复制到驱动程序的源目录。

接下来，驱动程序文件、 库文件、 规则的代码 (*RuleName*.slic) 文件和操作系统模型文件链接到单个可执行文件进行验证。

SDV 验证引擎然后验证一次，直到它将验证所有选定的规则的一条规则。

在此步骤中，SDV 创建其验证中的每个规则的子目录*DriverPath*\\sdv\\检查目录。

### <a name="span-idcommentspanspan-idcommentspancomment"></a><span id="comment"></span><span id="COMMENT"></span>注释

虽然 SDV 执行验证过程中的步骤，它将状态消息写入命令行中，以及错误消息会出现该报告错误中每个步骤。 有关状态消息的信息，请参阅[命令行输出](command-line-output.md)。 有关错误消息的信息，请参阅[静态 Driver Verifier 错误消息](static-driver-verifier-error-messages.md)。 有关启用诊断以帮助你和 Microsoft SDV 的疑难解答信息，请参阅[静态驱动程序验证工具诊断](static-driver-verifier-diagnostics.md)。

 

 





