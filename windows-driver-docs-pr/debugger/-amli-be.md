---
title: amli
description: Amli 为 extension 启用 AML 断点。
keywords:
- amli 是 Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli be
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b165a7a684e1f8a400f112659a71f13d4ba993ee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800121"
---
# <a name="amli-be"></a>!amli be

**！ Amli 为** EXTENSION 启用 AML 断点。

语法

```dbgcmd
    !amli be Breakpoint!amli be *
```

## <a name="span-idddk__amli_be_dbgspanspan-idddk__amli_be_dbgspanparameters"></a><span id="ddk__amli_be_dbg"></span><span id="DDK__AMLI_BE_DBG"></span>参数

<span id="_______Breakpoint______"></span><span id="_______breakpoint______"></span><span id="_______BREAKPOINT______"></span>*断点* 指定要启用的断点的断点号。

<span id="______________"></span> **\** _ 指定应启用所有断点。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令及其用法的信息，请参阅 [AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

所有断点在创建时都处于启用状态。 仅当已使用 [_ *！ amli bd* *](-amli-bd.md)扩展时，才会禁用断点。

若要确定断点的断点号，请使用 [**！ amli bl**](-amli-bl.md) 扩展。
