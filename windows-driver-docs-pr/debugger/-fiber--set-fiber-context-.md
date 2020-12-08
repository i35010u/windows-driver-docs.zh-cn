---
title: .fiber（设置光纤上下文）
description: 纤程命令指定要为纤程上下文使用哪种纤程。
keywords:
- " ( 纤程) 命令设置纤程上下文"
- context， ( 纤程上下文设置为纤程) 命令
- 纤程
- 纤程 (设置纤程上下文) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .fiber (Set Fiber Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cb2b2f0cf6a5531b7fc3b8dc7d56abc12f61d860
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821703"
---
# <a name="fiber-set-fiber-context"></a>.fiber（设置光纤上下文）


**纤** 程命令指定要为纤程上下文使用哪种纤程。

```dbgcmd
.fiber [Address]
```

## <a name="span-idddk_meta_set_fiber_context_dbgspanspan-idddk_meta_set_fiber_context_dbgspanparameters"></a><span id="ddk_meta_set_fiber_context_dbg"></span><span id="DDK_META_SET_FIBER_CONTEXT_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定纤程的地址。 如果省略此参数或指定零，则纤程上下文将重置为当前光纤。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关进程上下文、注册上下文和本地上下文的详细信息，请参阅 [更改上下文](changing-contexts.md)。

 

 





