---
title: amli r
description: Amli r 扩展显示有关当前上下文或指定的上下文信息。
ms.assetid: 1a8977ed-a420-4f68-8580-8e7446075283
keywords:
- Windows 调试 amli r
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli r
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 28cb2523213a6987388c93c040a2f260ccb47a2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564700"
---
# <a name="amli-r"></a>!amli r


**！ Amli r**扩展显示有关当前上下文或指定的上下文信息。

语法

```dbgcmd
   !amli r [ContextAddress]
```

## <a name="span-idddkamlirdbgspanspan-idddkamlirdbgspanparameters"></a><span id="ddk__amli_r_dbg"></span><span id="DDK__AMLI_R_DBG"></span>参数


<span id="_______ContextAddress______"></span><span id="_______contextaddress______"></span><span id="_______CONTEXTADDRESS______"></span> *ContextAddress*   
指定要显示的上下文块的地址。 可以根据上下文块的地址**Ctxt**字段中[ **！ amli lc** ](-amli-lc.md)显示。 如果*ContextAddress*前缀为两个百分号 (**%%**)，它被解释为物理地址。 否则，它被解释为一个虚拟地址。 如果省略此参数，则会显示当前上下文。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关相关的命令及其用途的信息，请参阅[AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

AMLI 调试器会突然显示提示，这是否有用的命令，以使用。

例如，以下命令将显示该解释器的当前上下文：

```console
AMLI(? for help)-> r

Context=c18b4000*, Queue=00000000, ResList=00000000
ThreadID=c15a6618, Flags=00000010
StackTop=c18b5eec, UsedStackSize=276 bytes, FreeStackSize=7636 bytes
LocalHeap=c18b40c0, CurrentHeap=c18b40c0, UsedHeapSize=88 bytes
Object=\_WAK, Scope=\_WAK, ObjectOwner=c18b4108, SyncLevel=0
AsyncCallBack=ff06b5d0, CallBackData=0, CallBackContext=c99efddc

MethodObject=\_WAK
80e0ff5c: Local0=Unknown()
80e0ff70: Local1=Unknown()
80e0ff84: Local2=Unknown()
80e0ff98: Local3=Unknown()
80e0ffac: Local4=Unknown()
80e0ffc0: Local5=Unknown()
80e0ffd4: Local6=Unknown()
80e0ffe8: Local7=Unknown()
80e0e040: RetObj=Unknown()

Next AML Pointer: ffffffff80e630df:[\_WAK+16]

ffffffff80e630df : If(S4BW
ffffffff80e630e5 : {
ffffffff80e630e5 : | Store(Zero, S4BW)
ffffffff80e630eb : }
```

 

 





