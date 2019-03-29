---
title: pt（步进到下一个 Return）
description: Pt 命令执行程序，直到达到返回指令。
ms.assetid: f4388953-4cb2-4df5-af8b-150e50ce765b
keywords:
- pt （到下一步返回的步骤） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pt (Step to Next Return)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0dd03c8e5e5ffd01875c2b31a439d9acc4b0c929
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567779"
---
# <a name="pt-step-to-next-return"></a>pt（步进到下一个 Return）


**Pt**命令执行程序，直到达到返回指令。

User-Mode

```dbgcmd
[~Thread] pt [r] [= StartAddress] [Count] ["Command"]
```

Kernel-Mode

```dbgcmd
pt [r] [= StartAddress] [Count] ["Command"]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
指定线程继续执行。 所有其他线程均已冻结。 有关语法的详细信息，请参阅[线程语法](thread-syntax.md)。 仅在用户模式下，可以指定线程。

<span id="_______r______"></span><span id="_______R______"></span> **r**   
开启和关闭显示器的寄存器和标志。 默认情况下，显示的寄存器和标志。 可以使用禁用注册显示**ptr**， [ **pr**](p--step-.md)， [ **tr**](t--trace-.md)，或.prompt\_允许-reg 命令。 所有这些命令控制的相同设置，可以使用其中任何一个重写任何以前使用这些命令。

此外可以使用 l os 命令来禁用注册显示。 此设置是独立于其他三个命令。 控制要显示的寄存器和标志，使用[ **rm （注册掩码）** ](rm--register-mask-.md)命令。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
指定调试器开始执行的位置的地址。 否则，调试器在指令指针指向的指令开始。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *Count*   
指定的数量**返回**必须遇到此命令可停止的说明。 默认值为 1。

<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span> *命令*   
指定要执行后执行步骤的调试器命令。 标准之前执行此命令**pt**显示结果。 如果还使用*计数*，指定的命令执行所有单步执行完毕后 （但之前的最后一步的结果会显示）。

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
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关相关命令的详细信息，请参阅[控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

**Pt**命令将导致目标开始执行。 此执行将继续，直至**返回**达到指令或遇到断点。

如果已经打开的程序计数器**返回**执行指令，整个返回。 返回此返回后，执行将继续，直到另一个**返回**为止。 此执行，而不是跟踪，在调用之间的唯一区别是**pt**并[ **tt (到下一步返回的 Trace)**](tt--trace-to-next-return-.md)。

在源模式中，可以将一个源行与多个程序集指令相关联。 **Pt**命令不会停止处**返回**与当前的源行相关联的指令。

下面的示例演示了如何使用**pt**命令连同**kb**命令以显示堆栈跟踪：

```dbgcmd
0:000> pt "kb"
```

 

 





