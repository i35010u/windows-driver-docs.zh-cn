---
title: amli 最佳实践
description: Amli bp 扩展 AML 代码中放置断点。
ms.assetid: 830df6b8-835c-4485-a28a-e9a028f166f5
keywords:
- Windows 调试 amli 最佳实践
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli bp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0b84fd4c9df4347cc9cf9915eb695fb20110c160
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337038"
---
# <a name="amli-bp"></a>!amli bp


**！ Amli bp**扩展 AML 代码中放置断点。

语法

```dbgcmd
    !amli bp { MethodName | CodeAddress }
```

## <a name="span-idddkamlibpdbgspanspan-idddkamlibpdbgspanparameters"></a><span id="ddk__amli_bp_dbg"></span><span id="DDK__AMLI_BP_DBG"></span>参数


<span id="_______MethodName______"></span><span id="_______methodname______"></span><span id="_______METHODNAME______"></span> *MethodName*   
指定将在其设置断点的方法名称的完整路径。

<span id="_______CodeAddress______"></span><span id="_______codeaddress______"></span><span id="_______CODEADDRESS______"></span> *CodeAddress*   
指定将在其中设置断点的 AML 代码的地址。 如果*CodeAddress*前缀为两个百分号 (**%%**)，它被解释为物理地址。 否则，它被解释为一个虚拟地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关相关的命令及其用途的信息，请参阅[AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

AMLI 调试器支持最多 10 个断点。

下面是一个示例。 以下命令将上设置断点\_DCK 方法：

```console
kd> !amli bp \_sb.pci0.dock._dck
```

 

 





