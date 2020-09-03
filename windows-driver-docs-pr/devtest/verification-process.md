---
title: 验证过程
description: 验证过程
ms.assetid: 3803771b-94ef-4e02-9d08-8703283b3f99
keywords:
- 静态驱动程序验证程序 WDK，验证过程
- StaticDV WDK，验证过程
- SDV WDK，验证过程
- 验证过程 WDK 静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 097c1267fe527435c00520ab8f6c2827e38f45a5
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89385075"
---
# <a name="verification-process"></a>验证过程


SDV 执行 *验证*，即确定驱动程序的实际行为是否符合定义正确行为的规则。

提交用于验证驱动程序的命令时，SDV 会执行三步过程，在此过程中，它将确定所需的文件，准备文件，并验证驱动程序。

本主题介绍验证过程的每个步骤中发生的情况。

### <a name="span-idbuildspanspan-idbuildspanbuild"></a><span id="build"></span><span id="BUILD"></span>生成

在 **生成** 步骤中，SDV 将编译和链接，并使用 MSBuild 生成驱动程序。

### <a name="span-idscanspanspan-idscanspanscan"></a><span id="scan"></span><span id="SCAN"></span>检测

在**扫描**步骤中，SDV 将扫描驱动程序的函数角色类型声明的代码，汇编驱动程序入口点列表，并在存储驱动程序*源文件*的目录中创建[SDV](sdv-map-h.md)文件， (称为**驱动程序的源目录**) 。

### <a name="span-idcheckspanspan-idcheckspancheck"></a><span id="check"></span><span id="CHECK"></span>查阅

在 **检查** 步骤中，SDV 通过使用为验证选择的规则来准备并验证驱动程序。 有关可选择的规则的详细信息，请参阅 [静态驱动程序验证程序规则](/windows-hardware/drivers/ddi/index)。

SDV 首先确定所选规则是否需要操作系统模型的附加组件。 如果是这样，SDV 会将其他操作系统模型文件复制到驱动程序的源目录。

接下来，驱动程序文件、库文件、规则代码 * (slic*) 文件和操作系统模型文件都链接到用于验证的单个可执行文件。

然后，SDV 验证引擎一次验证一个规则，直到验证所有选定的规则。

在此步骤中，SDV 将为它在*DriverPath* \\ SDV 检查目录中验证的每个规则创建一个子目录 \\ 。

### <a name="span-idcommentspanspan-idcommentspancomment"></a><span id="comment"></span><span id="COMMENT"></span>条

虽然 SDV 执行验证过程中的步骤，但它会将状态消息写入到命令行，并提供错误消息，报告每个步骤中发生的错误。 有关状态消息的信息，请参阅 [命令行输出](command-line-output.md)。 有关错误消息的信息，请参阅 [静态驱动程序验证程序错误消息](static-driver-verifier-error-messages.md)。 有关启用诊断以帮助你和 Microsoft 解决与 SDV 有关的问题的信息，请参阅 [静态驱动程序验证器诊断](static-driver-verifier-diagnostics.md)。

 

