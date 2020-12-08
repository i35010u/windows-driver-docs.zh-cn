---
title: .do
description: 在 C 中，do 标记的行为类似于 do 关键字，只是在条件之前不使用单词 "while"。
keywords:
- 。是否进行 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .do
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a7c24abe4a3047746ca79f9e75f4acea7888afc6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805865"
---
# <a name="do"></a>.do


在 C 中， **do** 标记的行为类似于 **do** 关键字，只是在条件之前不使用单词 "while"。

```dbgcmd
.do { Commands } (Condition) 
```

## <a name="span-idddk_token_do_dbgspanspan-idddk_token_do_dbgspansyntax-elements"></a><span id="ddk_token_do_dbg"></span><span id="DDK_TOKEN_DO_DBG"></span>语法元素


<span id="_______Commands______"></span><span id="_______commands______"></span><span id="_______COMMANDS______"></span>*命令*   
指定一个或多个命令，只要条件为 true，就会重复执行此命令，但将始终执行至少一次。 此命令块需要括在大括号中，即使它包含单个命令也是如此。 应该用分号分隔多个命令，但右大括号前的最后一个命令无需后跟分号。

<span id="_______Condition______"></span><span id="_______condition______"></span><span id="_______CONDITION______"></span>*条件*   
指定条件。 如果此值为零，则将其视为 false;否则为 true。 括号中的封闭 *条件* 是可选的。 *Condition* 必须是表达式，而不能是调试器命令。 它将通过默认表达式计算器 (MASM 或 c + +) 进行计算。 有关详细信息，请参阅 [数值表达式语法](numerical-expression-syntax.md)。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关其他控制流令牌及其在调试器命令程序中的使用的信息，请参阅 [使用调试器命令程序](using-debugger-command-programs.md)。

<a name="remarks"></a>备注
-------

[**Break**](https://support.microsoft.com/help/833721/available-switch-options-for-the-windows-xp-and-the-windows-server-200)和 [**. continue**](-continue.md)标记可用于退出或重新启动 *命令* 块。

 

