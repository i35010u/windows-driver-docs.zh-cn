---
title: amli 最佳实践
description: Amli bp 扩展在 AML 代码中放置一个断点。
keywords:
- amli bp Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli bp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8da6c084a0b8fbd963a519933d1eb7633c200255
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800107"
---
# <a name="amli-bp"></a>!amli bp


**！ Amli bp** 扩展在 AML 代码中放置一个断点。

语法

```dbgcmd
    !amli bp { MethodName | CodeAddress }
```

## <a name="span-idddk__amli_bp_dbgspanspan-idddk__amli_bp_dbgspanparameters"></a><span id="ddk__amli_bp_dbg"></span><span id="DDK__AMLI_BP_DBG"></span>参数


<span id="_______MethodName______"></span><span id="_______methodname______"></span><span id="_______METHODNAME______"></span>*方法名称*   
指定将在其上设置断点的方法名称的完整路径。

<span id="_______CodeAddress______"></span><span id="_______codeaddress______"></span><span id="_______CODEADDRESS______"></span>*CodeAddress*   
指定将在其上设置断点的 AML 代码的地址。 如果 *CodeAddress* 以两个百分号 (**%%**) ，则会将其解释为物理地址。 否则，会将其解释为虚拟地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令及其用法的信息，请参阅 [AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

AMLI 调试器最多支持10个断点。

示例如下。 以下命令将在 DCK 方法上设置断点 \_ ：

```console
kd> !amli bp \_sb.pci0.dock._dck
```

 

 





