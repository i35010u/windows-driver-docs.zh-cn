---
title: amli u
description: Amli u 扩展 unassembles AML 代码。
keywords:
- amli u Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli u
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: aa35e3203ab1a14375c320916ec4081a87026023
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800051"
---
# <a name="amli-u"></a>!amli u


**！ Amli u** 扩展 unassembles AML 代码。

语法

```dbgcmd
    !amli u [ MethodName | CodeAddress ]
```

## <a name="span-idddk__amli_u_dbgspanspan-idddk__amli_u_dbgspanparameters"></a><span id="ddk__amli_u_dbg"></span><span id="DDK__AMLI_U_DBG"></span>参数


<span id="_______MethodName______"></span><span id="_______methodname______"></span><span id="_______METHODNAME______"></span>*方法名称*   
指定要反汇编的方法名称的完整路径。

<span id="_______CodeAddress______"></span><span id="_______codeaddress______"></span><span id="_______CODEADDRESS______"></span>*CodeAddress*   
指定将开始反汇编的 AML 代码的地址。 如果 *CodeAddress* 以两个百分号 (**%%**) ，则会将其解释为物理地址。 否则，会将其解释为虚拟地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令及其用法的信息，请参阅 [AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

如果既没有指定 *方法名称* ，也没有指定 *CodeAddress* ，则从 AMLI 发出此命令

反汇编显示将继续，直到到达方法的末尾。

**注意**   标准 [**u (Unassemble)**](u--unassemble-.md) 命令不会通过 AML 代码提供正确的结果。

 

下面是一些示例。 若要在 address 0x80E5D701 上反汇编对象，请使用以下命令：

```console
kd> !amli u 80e5d701

ffffffff80e5d701 : CreateWordField(CRES, 0x1, IRQW)
ffffffff80e5d70c : And(\_SB_.PCI0.LPC_.PIRA, 0xf, Local0)
ffffffff80e5d723 : Store(One, Local1)
ffffffff80e5d726 : ShiftLeft(Local1, Local0, IRQW)
ffffffff80e5d72d : Return(CRES)
```

以下命令将反汇编 \_ DCK 方法：

```console
kd> u \_sb.pci0.dock._dck
```

 

 





