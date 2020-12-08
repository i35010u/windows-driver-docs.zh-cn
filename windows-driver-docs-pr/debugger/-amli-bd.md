---
title: amli bd
description: Amli bd 扩展暂时禁用 AML 断点。
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
ms.openlocfilehash: 5edd49544f58e415716be3b4e0835750964b2ace
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800123"
---
# <a name="amli-bd"></a>!amli bd

**！ Amli bd** extension 暂时禁用 AML 断点。

语法

```dbgcmd
    !amli bd Breakpoint!amli bd *
```

## <a name="span-idddk__amli_bd_dbgspanspan-idddk__amli_bd_dbgspanparameters"></a><span id="ddk__amli_bd_dbg"></span><span id="DDK__AMLI_BD_DBG"></span>参数

<span id="_______Breakpoint______"></span><span id="_______breakpoint______"></span><span id="_______BREAKPOINT______"></span>*断点* 指定要禁用的断点号。

<span id="______________"></span> **\** _ 指定应禁用所有断点。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令及其用法的信息，请参阅 [AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

可以使用 [_ *！ amli 作为* *](-amli-be.md)扩展名重新启用已禁用的断点。

若要确定断点的断点号，请使用 [**！ amli bl**](-amli-bl.md) 扩展。

下面是此命令的示例：

```console
kd> !amli bl
 0:  c29accf5 [\_WAK]
 1:  c29c20a5 [\_SB.PCI0.ISA.BAT1._BST]

kd> !amli bd 1
```
