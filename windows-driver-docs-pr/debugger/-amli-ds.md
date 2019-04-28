---
title: amli ds
description: Amli ds 扩展显示 AML 堆栈。
ms.assetid: 62a1a1dd-c0d8-4509-a29f-16ad2b96b412
keywords:
- amli ds Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli ds
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bfc0817c355b763646b49e0fa6515736042184a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337040"
---
# <a name="amli-ds"></a>!amli ds


**！ Amli ds**扩展显示 AML 堆栈。

语法

```dbgcmd
    !amli ds [/v] [Address] 
```

## <a name="span-idddkamlidsdbgspanspan-idddkamlidsdbgspanparameters"></a><span id="ddk__amli_ds_dbg"></span><span id="DDK__AMLI_DS_DBG"></span>参数


<span id="________v______"></span><span id="________V______"></span> **/v**   
将导致显示详细信息。 在 Windows 2000 中，此选项才可用，仅当使用此扩展已检验的版本 (w2kchk\\Acpikd.dll)。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定其堆栈所需的上下文块的地址。 如果*地址*是省略，则使用当前上下文。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

！ 堆栈扩展显示有关内核堆栈的信息。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关相关的命令及其用途的信息，请参阅[AMLI 调试器](the-amli-debugger.md)。

 

 





