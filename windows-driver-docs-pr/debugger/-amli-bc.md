---
title: amli 业务连续性
description: Amli 扩展永久清除 AML 断点的业务连续性。
ms.assetid: e975ee10-cd2f-4944-8d00-b2eda2dd099a
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
ms.openlocfilehash: f4b9dd7474b5a1c15b843587cd0bb54d09e12cbd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547444"
---
# <a name="amli-bc"></a>！ amli 业务连续性


**！ Amli bc**扩展永久清除 AML 断点。

语法

```dbgcmd
    !amli bc Breakpoint 
    !amli bc *
```

## <a name="span-idddkamlibcdbgspanspan-idddkamlibcdbgspanparameters"></a><span id="ddk__amli_bc_dbg"></span><span id="DDK__AMLI_BC_DBG"></span>参数


<span id="_______Breakpoint______"></span><span id="_______breakpoint______"></span><span id="_______BREAKPOINT______"></span> *Breakpoint*   
指定要清除的断点的数目。

<span id="______________"></span> **\\***   
指定应该清除所有断点。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关相关的命令及其用途的信息，请参阅[AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

若要确定断点的断点号，请使用[ **！ amli bl** ](-amli-bl.md)扩展。

 

 





