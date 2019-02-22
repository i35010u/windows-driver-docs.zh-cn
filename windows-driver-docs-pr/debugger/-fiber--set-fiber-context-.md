---
title: .fiber （设置纤程上下文）
description: .Fiber 命令指定哪些纤程使用纤程上下文。
ms.assetid: 37473c90-018c-417f-a2b2-3723b9d03ca7
keywords:
- 设置纤程上下文 (.fiber) 命令
- 上下文中，设置纤程上下文 (.fiber) 命令
- 纤程
- .fiber （设置纤程上下文） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .fiber (Set Fiber Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b6a637c508e4fb708514cedc6758bc3f8e14904a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534710"
---
# <a name="fiber-set-fiber-context"></a>.fiber （设置纤程上下文）


**.Fiber**命令指定哪些纤程使用纤程上下文。

```dbgcmd
.fiber [Address]
```

## <a name="span-idddkmetasetfibercontextdbgspanspan-idddkmetasetfibercontextdbgspanparameters"></a><span id="ddk_meta_set_fiber_context_dbg"></span><span id="DDK_META_SET_FIBER_CONTEXT_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定纤程的地址。 如果省略此参数或指定为零，则会将纤程上下文重置为当前的纤程。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关进程上下文、 寄存器上下文和本地上下文的详细信息，请参阅[更改上下文](changing-contexts.md)。

 

 





