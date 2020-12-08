---
title: amli dns
description: Amli dns 扩展显示 ACPI 命名空间对象。
keywords:
- amli dns Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli dns
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fc61967fb0211881183c4da6444d76ffe8f0a1d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800087"
---
# <a name="amli-dns"></a>!amli dns


**！ Amli dns** 扩展显示 ACPI 命名空间对象。

语法

```dbgcmd
    !amli dns [/s] [Name | Address]
```

## <a name="span-idddk__amli_dns_dbgspanspan-idddk__amli_dns_dbgspanparameters"></a><span id="ddk__amli_dns_dbg"></span><span id="DDK__AMLI_DNS_DBG"></span>参数


<span id="________s______"></span><span id="________S______"></span>**/s**   
导致以递归方式显示指定对象下的整个命名空间子树。

<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span>*名称*   
指定命名空间路径。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定命名空间节点的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令及其用法的信息，请参阅 [AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

如果 *名称* 和 *地址* 均未指定，则将以递归方式显示整个 ACPI 命名空间树。 在这种情况下，始终假定 **/s** 参数，即使未指定此参数。

此命令可用于确定特定的命名空间对象是什么，无论该对象是方法、字段单位、设备还是其他类型的对象。

如果没有 **/s** 参数，此扩展等效于 [**！ nsobj**](-nsobj.md) 扩展名。 对于 **/s** 参数，它等效于 [**！ nstree**](-nstree.md) 扩展名。

下面是一些示例。 以下命令显示对象 **bios** 的命名空间：

```console
AMLI(? for help)-> dns \bios

ACPI Name Space: \BIOS (80E5F378)
OpRegion(BIOS:RegionSpace=SystemMemory,Offset=0xfcb07500,Len=2816)
```

以下命令显示对象 BST 的命名空间 \_ ，以及该对象的子树：

```console
kd> !amli dns /s \_sb.pci0.isa.bat1._bst

ACPI Name Space: \_SB.PCI0.ISA.BAT1._BST (c29c2044)
Method(_BST:Flags=0x0,CodeBuff=c29c20a5,Len=103)
```

若要显示设备 BAT1 的命名空间，请键入：

```console
kd> !amli dns /s \_sb.pci0.isa.bat1
```

若要显示从属于停靠设备的所有内容的命名空间，请键入：

```console
kd> !amli dns /s \_sb.pci0.dock
```

若要显示 DCK 方法的从属命名空间 \_ ，请键入：

```console
kd> !amli dns /s \_sb.pci0.dock._dck
```

若要显示整个命名空间，请键入：

```console
kd> !amli dns
```

 

 





