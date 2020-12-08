---
title: amli 调试器
description: Amli 调试器扩展将进入 AMLI 调试器。
keywords:
- amli 调试器 Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli debugger
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ce45b2cfd55a0fc05bbc8dc32ac517425cbc6727
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800101"
---
# <a name="amli-debugger"></a>!amli debugger


**！ Amli 调试器** 扩展将进入 amli 调试器。

语法

```dbgcmd
    !amli debugger
```

## <span id="ddk__amli_debugger_dbg"></span><span id="DDK__AMLI_DEBUGGER_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令及其用法的信息，请参阅 [AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

发出此命令时，会将通知发送到 AML 解释器。 下一次激活解释器时，它会立即中断到 AMLI 调试器。

**！ Amli 调试器** 扩展仅导致一次中断。 如果希望再次中断，则需要再次使用此扩展，或设置断点。

 

 





