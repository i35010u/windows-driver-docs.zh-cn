---
title: amli bd
description: Amli bd 扩展可临时禁用 AML 断点。
ms.assetid: a7fb4f51-8984-425b-858d-1e1e69825891
keywords:
- Windows 调试 amli bd
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli bd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ba99828d281e9ec87561bd1aa9860faf5c84de32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334778"
---
# <a name="amli-bd"></a>!amli bd


**！ Amli bd**扩展可临时禁用 AML 断点。

语法

```dbgcmd
    !amli bd Breakpoint!amli bd *
```

## <a name="span-idddkamlibddbgspanspan-idddkamlibddbgspanparameters"></a><span id="ddk__amli_bd_dbg"></span><span id="DDK__AMLI_BD_DBG"></span>参数


<span id="_______Breakpoint______"></span><span id="_______breakpoint______"></span><span id="_______BREAKPOINT______"></span> *Breakpoint*   
指定要禁用的断点的数目。

<span id="______________"></span> **\\***   
指定应禁用所有断点。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关相关的命令及其用途的信息，请参阅[AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

可以通过重新启用已禁用的断点[ **！ amli 会**](-amli-be.md)扩展。

若要确定断点的断点号，请使用[ **！ amli bl** ](-amli-bl.md)扩展。

下面是此命令的示例：

```console
kd> !amli bl
 0:  c29accf5 [\_WAK]
 1:  c29c20a5 [\_SB.PCI0.ISA.BAT1._BST]

kd> !amli bd 1
```

 

 





