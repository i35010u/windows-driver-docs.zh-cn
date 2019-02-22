---
title: .apply_dbp （适用于上下文的数据断点）
description: .Apply_dbp 命令适用于指定的寄存器上下文当前进程的现有数据断点。
ms.assetid: c74fd4b3-3335-4e03-a57a-6a9aa883dd9f
keywords:
- .apply_dbp （适用于上下文的数据断点） Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- .apply_dbp (Apply Data Breakpoint to Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5b86c00a0c785ae6f52172f918b076148eb1ef6d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543072"
---
# <a name="applydbp-apply-data-breakpoint-to-context"></a>.apply\_dbp （到上下文应用数据断点）


**.Apply\_dbp**命令将当前进程的现有数据断点应用于指定的寄存器上下文。

```dbgcmd
    .apply_dbp [/m Context] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="________m_______Context______"></span><span id="________m_______context______"></span><span id="________M_______CONTEXT______"></span> **/m** *上下文*   
指定要对其应用当前进程的数据断点的内存中寄存器上下文 （CONTEXT 结构） 的地址。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式和内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时目标</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关控制处理器的断点的详细信息，请参阅[处理器断点 (ba 断点)](processor-breakpoints---ba-breakpoints-.md)。 有关寄存器上下文 （线程上下文） 的详细信息，请参阅[注册上下文](changing-contexts.md#register-context)。

<a name="remarks"></a>备注
-------

调用由处理器控制的断点*数据断点*或*处理器断点*。 创建这些断点[ **ba （中断的访问权限）** ](ba--break-on-access-.md)命令。

遇到这些断点与相关联的特定进程的地址空间中的内存位置。 **.Apply\_dbp**命令将修改指定的寄存器上下文，以便使用此上下文时，这些数据断点将处于活动状态。

如果 **/m** *地址*未使用参数时，数据断点将应用于当前寄存器上下文。

如果目标是在本机模式下，仅可以使用此命令。 例如，如果目标模拟 x86 的 64 位计算机上运行使用处理器*WOW64*，不能使用此命令。

此命令很有用的一个示例是时间的在异常筛选器。 **.Apply\_dbp**命令可以更新异常筛选器的存储的上下文。 当异常筛选器退出，并恢复将存储的上下文，然后将应用数据断点。 如果没有这种修改很可能会丢失数据断点。

 

 





