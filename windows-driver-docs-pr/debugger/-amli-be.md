---
title: amli 是
description: Amli 是扩展使 AML 断点。
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
ms.openlocfilehash: dc978d103915560d5fd62f111678fe43645bb97c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540404"
---
# <a name="amli-be"></a>！ amli 是


**！ Amli 是**扩展使 AML 断点。

语法

```dbgcmd
    !amli be Breakpoint!amli be *
```

## <a name="span-idddkamlibedbgspanspan-idddkamlibedbgspanparameters"></a><span id="ddk__amli_be_dbg"></span><span id="DDK__AMLI_BE_DBG"></span>参数


<span id="_______Breakpoint______"></span><span id="_______breakpoint______"></span><span id="_______BREAKPOINT______"></span> *Breakpoint*   
指定要启用的断点的断点数。

<span id="______________"></span> **\\***   
指定应启用所有断点。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关相关的命令及其用途的信息，请参阅[AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

在创建时启用所有断点。 你已使用才会禁用断点[ **！ amli bd** ](-amli-bd.md)扩展。

若要确定断点的断点号，请使用[ **！ amli bl** ](-amli-bl.md)扩展。

 

 





