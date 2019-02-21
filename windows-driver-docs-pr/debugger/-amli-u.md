---
title: amli u
description: Amli u 扩展名 unassembles AML 代码。
ms.assetid: 0a8b160f-9aae-4ef0-a569-8e701de9679c
keywords:
- Windows 调试 amli u
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli u
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5881f44ea1d07c28f0597561a5586402a49df28d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521557"
---
# <a name="amli-u"></a>！ amli u


**！ Amli u**扩展 unassembles AML 代码。

语法

```dbgcmd
    !amli u [ MethodName | CodeAddress ]
```

## <a name="span-idddkamliudbgspanspan-idddkamliudbgspanparameters"></a><span id="ddk__amli_u_dbg"></span><span id="DDK__AMLI_U_DBG"></span>参数


<span id="_______MethodName______"></span><span id="_______methodname______"></span><span id="_______METHODNAME______"></span> *MethodName*   
指定方法名称要拆装的完整路径。

<span id="_______CodeAddress______"></span><span id="_______codeaddress______"></span><span id="_______CODEADDRESS______"></span> *CodeAddress*   
指定的地址的反汇编开始的位置的 AML 代码。 如果*CodeAddress*前缀为两个百分号 (**%%**)，它被解释为物理地址。 否则，它被解释为一个虚拟地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关相关的命令及其用途的信息，请参阅[AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

如果既没有*MethodName*也不*CodeAddress*指定并在从 AMLI 发出此命令

反汇编显示将继续，直到到达该方法的末尾。

**请注意**  标准[ **u （反汇编）** ](u--unassemble-.md)命令不会给正确的结果，使用 AML 代码。

 

下面是一些示例。 若要反汇编 0x80E5D701 地址处的对象，请使用以下命令：

```console
kd> !amli u 80e5d701

ffffffff80e5d701 : CreateWordField(CRES, 0x1, IRQW)
ffffffff80e5d70c : And(\_SB_.PCI0.LPC_.PIRA, 0xf, Local0)
ffffffff80e5d723 : Store(One, Local1)
ffffffff80e5d726 : ShiftLeft(Local1, Local0, IRQW)
ffffffff80e5d72d : Return(CRES)
```

以下命令将反汇编\_DCK 方法：

```console
kd> u \_sb.pci0.dock._dck
```

 

 





