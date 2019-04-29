---
title: 审批 Sdv-map.h 文件
description: 审批 Sdv-map.h 文件
ms.assetid: eb192eb2-7a2c-47eb-846e-3d641d5046a8
keywords:
- Sdv map.h WDK Static Driver Verifier，批准
- 批准 Sdv map.h
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65e1ac75efd01e57684a09fd11ff386c47b46a26
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361309"
---
# <a name="approving-the-sdv-maph-file"></a>审批 Sdv-map.h 文件


Sdv map.h 文件包含告知 SDV 之后检查该文件并更正任何错误可能批准该文件的文本行。 在创建时的 Sdv map.h 文件包括短语："批准 = false。"

### <a name="span-idtoapproveansdvmaphfilespanspan-idtoapproveansdvmaphfilespanto-approve-an-sdv-maph-file"></a><span id="to_approve_an_sdv_map_h_file"></span><span id="TO_APPROVE_AN_SDV_MAP_H_FILE"></span>若要批准的 Sdv map.h 文件

1.  在诸如记事本之类的文本编辑器中打开 Sdv map.h 文件。 SDV 驱动程序的源目录中创建的 Sdv map.h 文件。 （它是一次验证的本地目录。）

2.  更改 **//Approved=false**到 **//Approved=true**。

### <a name="span-idwhenyoushouldapproveasdvmaphfilespanspan-idwhenyoushouldapproveasdvmaphfilespanwhen-you-should-approve-a-sdv-maph-file"></a><span id="when_you_should_approve_a_sdv_map_h_file"></span><span id="WHEN_YOU_SHOULD_APPROVE_A_SDV_MAP_H_FILE"></span>你应批准 Sdv map.h 文件

Sdv map.h 时才能进行正确和完整 SDV:

-   找到的所有入口点，使用它。

-   已与正确的函数角色类型关联的入口点。

### <a name="span-idwhenyoushouldcorrectasdvmaphfilespanspan-idwhenyoushouldcorrectasdvmaphfilespanwhen-you-should-correct-a-sdv-maph-file"></a><span id="when_you_should_correct_a_sdv_map_h_file"></span><span id="WHEN_YOU_SHOULD_CORRECT_A_SDV_MAP_H_FILE"></span>当应更正的 Sdv map.h 文件

Sdv map.h 文件不正确或不完整时 SDV:

-   未检测到任何入口点驱动程序，通常是因为它找不到函数角色类型声明 (请参阅[使用函数角色类型声明](using-function-role-type-declarations.md))。

-   重复的回调函数都有一种函数角色类型关联。

-   具有函数角色类型支持多个回调函数超出了上限。

-   已检测到错误或不存在的函数名称 Sdv map.h 文件中之后有该文件已批准。

驱动程序不需要具有 SDV 可以分析每个入口点。 如果验证的特定规则需要一个驱动程序入口点，该驱动程序不具有，SDV 取消该规则的验证并返回的结果**不适用**。 此结果不被视为可失败的结果。

除非 SDV 找不到驱动程序中的任何入口点，它将继续进行分析。 如果在分析中使用的标头文件是不完整或不正确，则验证结果不可靠。

SDV 检测到存在错误或不存在的函数名称 Sdv map.h 文件中批准该文件后，如果 SDV 退出，并发出警告消息，如下例所示：

```
Warning 'driver' It appears that your sdv-map.h file has an incorrect entry at this line "#define fun_IRP_MJ_PNP DispatchPnpNotExist". Please regenerate your sdv-map.h file.
```

若要修复此错误，删除 Sdv.map 文件中导致错误或重新生成文件的行。

### <a name="span-idtoregeneratethesdvmaphfilespanspan-idtoregeneratethesdvmaphfilespanto-regenerate-the-sdv-maph-file"></a><span id="to_regenerate_the_sdv_map_h_file"></span><span id="TO_REGENERATE_THE_SDV_MAP_H_FILE"></span>若要重新生成 Sdv map.h 文件

1.  打开 Sdv map.h 文件并更改 **//Approved=true**到 **//Approved=false**。

2.  使用**staticdv /scan**命令来重新生成映射文件中，或使用**staticdv /rule**或**staticdv /config**命令以运行 SDV 分析。

 

 





