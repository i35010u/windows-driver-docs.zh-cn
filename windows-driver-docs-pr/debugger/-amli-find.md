---
title: amli 查找
description: Amli 查找扩展可查找 ACPI 命名空间对象。
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
ms.openlocfilehash: 9ae27491645eb64d39c861677ec4f454165b69b7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800079"
---
# <a name="amli-find"></a>!amli find


**！ Amli 查找** 扩展可查找 ACPI 命名空间对象。

语法

```dbgcmd
    !amli find Name
```

## <a name="span-idddk__amli_find_dbgspanspan-idddk__amli_find_dbgspanparameters"></a><span id="ddk__amli_find_dbg"></span><span id="DDK__AMLI_FIND_DBG"></span>参数


<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span>*名称*   
指定不具有路径)  (命名空间对象的名称。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令及其用法的信息，请参阅 [AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

**！ Amli find** 命令使用对象的名称，并返回完整的路径和名称。 *Name* 参数必须是完整路径和名称的最后一个段。

下面是一些示例。 以下命令将查找对象 SRS 的所有声明 \_ ：

```console
kd> !amli find _srs
\_SB.LNKA._SRS
\_SB.LNKB._SRS
\_SB.LNKC._SRS
\_SB.LNKD._SRS
```

这不仅仅是文本搜索。 命令 **！ amli find srs** 不显示任何命中，因为其中每个声明的最后一段是 " \_ srs"，而不是 "srs"。 命令 **！ amli FIND .lnk** 类似地不返回命中。 命令 **！ amli FIND LNKB** 会显示以 "LNKB" 终止的单个节点，而不是显示在前面的显示中的此节点的四个子节点：

```console
kd> !amli find lnkb
\_SB.LNKB.
```

如果需要查看节点的子节点，请使用带有 **/s** 参数的 [**！ amli dns**](-amli-dns.md)命令。

下面是另一个示例，通过 AMLI 调试器提示符发出。 这会显示 \_ 命名空间中对象 BST 的所有声明：

```console
AMLI(? for help)-> find _bst
\_SB.PCI0.ISA.BAT1._BST
\_SB.PCI0.ISA.BAT2._BST
```

 

 





