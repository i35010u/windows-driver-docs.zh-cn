---
title: .apply_dbp（将数据断点应用到上下文）
description: .Apply_dbp 命令将当前进程的现有数据断点应用到指定的寄存器上下文。
keywords:
- .apply_dbp (将数据断点应用于上下文) Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- .apply_dbp (Apply Data Breakpoint to Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5d254b5e04dc647d6b824a98135fa43db39ed83f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800031"
---
# <a name="apply_dbp-apply-data-breakpoint-to-context"></a>。应用 \_ .dbp (将数据断点应用于上下文) 


" **应用" \_ "应用** " "应用" "应用" "应用"。

```dbgcmd
    .apply_dbp [/m Context] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="________m_______Context______"></span><span id="________m_______context______"></span><span id="________M_______CONTEXT______"></span>**/M** *上下文*   
指定注册上下文的地址 (上下文结构) 在内存中，以便应用当前进程的数据断点。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式和内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限活动目标</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关处理器控制的断点的详细信息，请参阅 [处理器断点 (Ba 断点) ](processor-breakpoints---ba-breakpoints-.md)。 有关注册上下文 (线程上下文) 的详细信息，请参阅 [注册上下文](changing-contexts.md#register-context)。

<a name="remarks"></a>备注
-------

由处理器控制的断点称为 *数据断点* 或 *处理器断点*。 这些断点由 [**ba (Access)**](ba--break-on-access-.md) 命令创建。

这些断点与特定进程的地址空间中的内存位置相关联。 **. 应用 \_ .dbp** 命令修改指定的寄存器上下文，以便在使用此上下文时这些数据断点将处于活动状态。

如果未使用 **/M** *Address* 参数，则数据断点将应用于当前的注册上下文。

仅当目标为纯计算机模式时，才能使用此命令。 例如，如果目标是在使用 *WOW64* 模拟 x86 处理器的64位计算机上运行，则不能使用此命令。

此命令的一个示例就是在异常筛选器中。 **. 应用 \_ .dbp** 命令可以更新异常筛选器的存储上下文。 然后，在异常筛选器退出并恢复存储的上下文时，将应用数据断点。 如果没有此类修改，则可能会丢失数据断点。

 

 





