---
title: amli ln
description: Amli ln 扩展显示指定的方法或包含给定地址的方法。
keywords:
- amli ln Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli ln
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dcbf284de8a57c5a7d3054a88d387d8590b0f028
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800065"
---
# <a name="amli-ln"></a>!amli ln


**！ Amli ln** 扩展显示指定的方法或包含给定地址的方法。

语法

```dbgcmd
    !amli ln [ MethodName | CodeAddress ]
```

## <a name="span-idddk__amli_ln_dbgspanspan-idddk__amli_ln_dbgspanparameters"></a><span id="ddk__amli_ln_dbg"></span><span id="DDK__AMLI_LN_DBG"></span>参数


<span id="_______MethodName______"></span><span id="_______methodname______"></span><span id="_______METHODNAME______"></span>*方法名称*   
指定方法名称的完整路径。 如果 *方法名称* 指定的对象不是实际方法，则会产生错误。

<span id="_______CodeAddress______"></span><span id="_______codeaddress______"></span><span id="_______CODEADDRESS______"></span>*CodeAddress*   
指定所需方法中包含的 AML 代码的地址。 如果 *CodeAddress* 以两个百分号 (**%%**) ，则会将其解释为物理地址。 否则，会将其解释为虚拟地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令及其用法的信息，请参阅 [AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

如果既没有指定方法 *名称* 也未指定 *CodeAddress* ，则将显示与当前上下文相关联的方法。

以下命令显示当前正在运行的方法：

```console
kd> !amli ln
c29accf5: \_WAK
```

\_显示 WAK 方法，地址为0xC29ACCF5。

 

 





