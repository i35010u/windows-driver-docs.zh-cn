---
title: amli 查找
description: Amli 查找扩展查找 ACPI 命名空间对象。
ms.assetid: bacb1be2-f079-49da-a8d2-1e9821b20ed3
keywords:
- amli 查找 Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli find
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 446c2f36f94500054a4022649dffebc2cd697e07
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565979"
---
# <a name="amli-find"></a>!amli find


**！ Amli 查找**扩展查找 ACPI 命名空间对象。

语法

```dbgcmd
    !amli find Name
```

## <a name="span-idddkamlifinddbgspanspan-idddkamlifinddbgspanparameters"></a><span id="ddk__amli_find_dbg"></span><span id="DDK__AMLI_FIND_DBG"></span>参数


<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span> *名称*   
指定的命名空间对象 （不带路径） 的名称。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关相关的命令及其用途的信息，请参阅[AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

**！ Amli 查找**命令将该对象的名称，并返回的完整路径和名称。 *名称*参数必须是最后一段的完整路径和名称。

下面是一些示例。 以下命令将查找的对象的所有声明\_SRS:

```console
kd> !amli find _srs
\_SB.LNKA._SRS
\_SB.LNKB._SRS
\_SB.LNKC._SRS
\_SB.LNKD._SRS
```

这不是只需文本搜索。 该命令 **！ amli 查找 srs**不显示任何命中数，因为每个这些声明的最后一段是"\_SRS"，不是"SRS"。 该命令 **！ amli 查找 LNK**同样不会返回命中数。 该命令 **！ amli 查找 LNKB**将显示在"LNKB"中不显示在上一中此节点的四个子级终止单个节点：

```console
kd> !amli find lnkb
\_SB.LNKB.
```

如果需要查看节点的子级，请使用[ **！ amli dns** ](-amli-dns.md)命令 **/s**参数。

下面是另一个示例中，从 AMLI 调试器发出提示。 这将显示对象的所有声明\_BST 的命名空间中：

```console
AMLI(? for help)-> find _bst
\_SB.PCI0.ISA.BAT1._BST
\_SB.PCI0.ISA.BAT2._BST
```

 

 





