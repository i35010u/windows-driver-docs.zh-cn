---
title: amli bc
description: Amli bc 扩展会永久清除 AML 断点。
keywords:
- amli bc Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli bc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 47b5058a981542d0f06d3d8d720b87e5774b4927
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800125"
---
# <a name="amli-bc"></a>!amli bc

**！ Amli bc** 扩展会永久清除 AML 断点。

语法

```dbgcmd
    !amli bc Breakpoint
    !amli bc *
```

## <a name="span-idddk__amli_bc_dbgspanspan-idddk__amli_bc_dbgspanparameters"></a><span id="ddk__amli_bc_dbg"></span><span id="DDK__AMLI_BC_DBG"></span>参数

<span id="_______Breakpoint______"></span><span id="_______breakpoint______"></span><span id="_______BREAKPOINT______"></span>*断点* 指定要清除的断点号。

<span id="______________"></span> **\** _ 指定应清除所有断点。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令及其用法的信息，请参阅 [AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

若要确定断点的断点号，请使用 [_ *！ amli bl* *](-amli-bl.md)扩展。
