---
title: amli 调试器
description: Amli 调试器扩展强行进入 AMLI 调试器。
ms.assetid: ef55a45f-445a-4b05-a2a9-b21be3667ec3
keywords:
- Windows 调试 amli 调试器
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli debugger
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4240f325201318ad8c90aa393544b89e16f8be2e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337020"
---
# <a name="amli-debugger"></a>!amli debugger


**！ Amli 调试器**扩展强行进入 AMLI 调试器。

语法

```dbgcmd
    !amli debugger
```

## <span id="ddk__amli_debugger_dbg"></span><span id="DDK__AMLI_DEBUGGER_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关相关的命令及其用途的信息，请参阅[AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

当发出此命令时，通知是发送给 AML 解释器。 下一次该解释器处于活动状态，它将立即进入 AMLI 调试器。

**！ Amli 调试器**扩展仅会导致一个中断。 如果你希望再次中断，需要再次使用此扩展插件或设置一个断点。

 

 





