---
title: amli bd
description: Amli bd 扩展暂时禁用 AML 断点。
ms.assetid: a7fb4f51-8984-425b-858d-1e1e69825891
keywords:
- amli bd Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli bd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 57c93d91a8ea5b94622b02b3bf75351fdad53627
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038038"
---
# <a name="amli-bd"></a>!amli bd

**！ Amli bd** extension 暂时禁用 AML 断点。

语法

```dbgcmd
    !amli bd Breakpoint!amli bd *
```

## <a name="span-idddk__amli_bd_dbgspanspan-idddk__amli_bd_dbgspanparameters"></a><span id="ddk__amli_bd_dbg"></span><span id="DDK__AMLI_BD_DBG"></span>Parameters

<span id="_______Breakpoint______"></span><span id="_______breakpoint______"></span><span id="_______BREAKPOINT______"></span>*断点*指定要禁用的断点号。

<span id="______________"></span> **\*** 指定应禁用所有断点。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令及其用法的信息，请参阅[AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

可以通过使用[ **！ amli 为**](-amli-be.md)extension 来重新启用已禁用的断点。

若要确定断点的断点号，请使用[ **！ amli bl**](-amli-bl.md)扩展。

下面是此命令的示例：

```console
kd> !amli bl
 0:  c29accf5 [\_WAK]
 1:  c29c20a5 [\_SB.PCI0.ISA.BAT1._BST]

kd> !amli bd 1
```
