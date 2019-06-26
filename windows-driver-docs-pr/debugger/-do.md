---
title: .do
description: 执行令牌的行为类似于 do 关键字在 C 中，只不过在条件之前未使用"while"一词。
ms.assetid: 254413bd-7fa5-4401-b242-470f9c0cf11a
keywords:
- 执行 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .do
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 436f77940bc50cb824df7a66e210e89cf2728529
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363163"
---
# <a name="do"></a>.do


**执行**令牌的行为类似于**执行**关键字在 C 中，只不过在条件之前未使用"while"一词。

```dbgcmd
.do { Commands } (Condition) 
```

## <a name="span-idddktokendodbgspanspan-idddktokendodbgspansyntax-elements"></a><span id="ddk_token_do_dbg"></span><span id="DDK_TOKEN_DO_DBG"></span>语法元素


<span id="_______Commands______"></span><span id="_______commands______"></span><span id="_______COMMANDS______"></span> *命令*   
指定一个或多个，只要条件为 true-但将始终执行至少一次重复执行的命令。 下面的命令块必须括在大括号，即使它包含单个命令。 之前的右大括号不需要后接分号，应由分号，但最后一个命令分隔的多个命令。

<span id="_______Condition______"></span><span id="_______condition______"></span><span id="_______CONDITION______"></span> *Condition*   
指定的条件。 如果此计算结果为零，则将其视为 false;否则为 true。 封闭*条件*在括号是可选的。 *条件*必须是一个表达式，而不是调试器命令。 默认表达式计算器将评估 (MASM 或C++)。 有关详细信息，请参阅[数值表达式语法](numerical-expression-syntax.md)。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关其他控制流令牌在调试器命令程序及其用法的信息，请参阅[使用调试器命令程序](using-debugger-command-programs.md)。

<a name="remarks"></a>备注
-------

[ **.Break** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/-break)并[ **.continue** ](-continue.md)令牌可用于退出或重新启动*命令*块。

 

 





