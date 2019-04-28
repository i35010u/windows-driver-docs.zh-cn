---
title: amli dns
description: Amli dns 扩展显示 ACPI 命名空间对象。
ms.assetid: 7db937ba-109f-4f4e-8dd3-4aa5d0dc13b2
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
ms.openlocfilehash: 1d05bafcb96bdd57130ee9d849edfebcea5d5ab3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334762"
---
# <a name="amli-dns"></a>!amli dns


**！ Amli dns**扩展显示 ACPI 命名空间对象。

语法

```dbgcmd
    !amli dns [/s] [Name | Address]
```

## <a name="span-idddkamlidnsdbgspanspan-idddkamlidnsdbgspanparameters"></a><span id="ddk__amli_dns_dbg"></span><span id="DDK__AMLI_DNS_DBG"></span>参数


<span id="________s______"></span><span id="________S______"></span> **/s**   
导致下要显示以递归方式的指定对象的整个命名空间子树。

<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span> *名称*   
指定的命名空间路径。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的命名空间节点的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关相关的命令及其用途的信息，请参阅[AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

如果既没有*名称*也不*地址*指定，则整个 ACPI 命名空间树是显示以递归方式。 **/S**即使未指定，始终这种情况下，假定参数。

此命令可用于确定特定命名空间对象是什么，它是一种方法、 字段单元、 一台设备或另一种类型的对象。

无需 **/s**参数，此扩展是等效于[ **！ nsobj** ](-nsobj.md)扩展。 与 **/s**参数，它等效于[ **！ nstree** ](-nstree.md)扩展。

下面是一些示例。 下面的命令显示对象的命名空间**bios**:

```console
AMLI(? for help)-> dns \bios

ACPI Name Space: \BIOS (80E5F378)
OpRegion(BIOS:RegionSpace=SystemMemory,Offset=0xfcb07500,Len=2816)
```

下面的命令显示对象的命名空间\_BST 和树从属到它：

```console
kd> !amli dns /s \_sb.pci0.isa.bat1._bst

ACPI Name Space: \_SB.PCI0.ISA.BAT1._BST (c29c2044)
Method(_BST:Flags=0x0,CodeBuff=c29c20a5,Len=103)
```

若要显示设备 BAT1 的命名空间，请键入：

```console
kd> !amli dns /s \_sb.pci0.isa.bat1
```

若要显示的所有内容从闸门设备属于命名空间，请键入：

```console
kd> !amli dns /s \_sb.pci0.dock
```

若要显示的命名空间属于\_DCK 方法，类型：

```console
kd> !amli dns /s \_sb.pci0.dock._dck
```

若要显示整个命名空间，请键入：

```console
kd> !amli dns
```

 

 





