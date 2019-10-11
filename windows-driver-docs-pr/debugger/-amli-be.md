---
title: amli
description: Amli 为 extension 启用 AML 断点。
ms.assetid: 75c0c05f-8c56-4489-a798-2e5ec6ca26d8
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
ms.openlocfilehash: a32c06d0706bd16a260b09d86f33ede99c0f327e
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038028"
---
# <a name="amli-be"></a>!amli be

**！ Amli 为**EXTENSION 启用 AML 断点。

语法

```dbgcmd
    !amli be Breakpoint!amli be *
```

## <a name="span-idddk__amli_be_dbgspanspan-idddk__amli_be_dbgspanparameters"></a><span id="ddk__amli_be_dbg"></span><span id="DDK__AMLI_BE_DBG"></span>Parameters

<span id="_______Breakpoint______"></span><span id="_______breakpoint______"></span><span id="_______BREAKPOINT______"></span>*断点*指定要启用的断点的断点号。

<span id="______________"></span> **\*** 指定应启用所有断点。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令及其用法的信息，请参阅[AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

所有断点在创建时都处于启用状态。 仅当已使用[ **！ amli bd**](-amli-bd.md)扩展时，才会禁用断点。

若要确定断点的断点号，请使用[ **！ amli bl**](-amli-bl.md)扩展。
