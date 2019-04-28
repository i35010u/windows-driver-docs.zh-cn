---
title: amli ln
description: Amli ln 扩展显示指定的方法或包含给定的地址的方法。
ms.assetid: f763f185-cce2-4bfb-948d-243acfb53aaa
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
ms.openlocfilehash: 34a302d69631437aa883d8c077aab7b516ce41ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334756"
---
# <a name="amli-ln"></a>!amli ln


**！ Amli ln**扩展显示指定的方法或包含给定的地址的方法。

语法

```dbgcmd
    !amli ln [ MethodName | CodeAddress ]
```

## <a name="span-idddkamlilndbgspanspan-idddkamlilndbgspanparameters"></a><span id="ddk__amli_ln_dbg"></span><span id="DDK__AMLI_LN_DBG"></span>参数


<span id="_______MethodName______"></span><span id="_______methodname______"></span><span id="_______METHODNAME______"></span> *MethodName*   
指定方法名称的完整路径。 如果*MethodName*指定不是实际的方法，产生错误的对象。

<span id="_______CodeAddress______"></span><span id="_______codeaddress______"></span><span id="_______CODEADDRESS______"></span> *CodeAddress*   
指定所需的方法中包含的 AML 代码的地址。 如果*CodeAddress*前缀为两个百分号 (**%%**)，它被解释为物理地址。 否则，它被解释为一个虚拟地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关相关的命令及其用途的信息，请参阅[AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

如果既没有*MethodName*也不*CodeAddress*指定，则会显示与当前上下文关联的方法。

下面的命令显示当前正在运行的方法：

```console
kd> !amli ln
c29accf5: \_WAK
```

该方法\_WAK 所示，使用地址 0xC29ACCF5。

 

 





