---
title: pt（步进到下一个 Return）
description: Pt 命令执行程序，直到到达返回指令。
keywords:
- pt (单步到下一步返回) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pt (Step to Next Return)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e15bb913752bc8cd2b2b8a60a02aa5eeeb853a7c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811205"
---
# <a name="pt-step-to-next-return"></a>pt（步进到下一个 Return）


**Pt** 命令执行程序，直到到达返回指令。

User-Mode

```dbgcmd
[~Thread] pt [r] [= StartAddress] [Count] ["Command"]
```

Kernel-Mode

```dbgcmd
pt [r] [= StartAddress] [Count] ["Command"]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
指定要继续执行的线程。 所有其他线程均已冻结。 有关语法的详细信息，请参阅 [线程语法](thread-syntax.md)。 只能在用户模式下指定线程。

<span id="_______r______"></span><span id="_______R______"></span>**r**   
打开和关闭寄存器和标志的显示。 默认情况下，将显示寄存器和标志。 您可以通过使用 **ptr**、 [**pr**](p--step-.md)、 [**tr**](t--trace-.md)或提示禁止注册显示 \_ 。 所有这些命令都控制相同的设置，你可以使用其中任何一个命令来替代以前使用的这些命令。

你还可以使用 l os 命令禁用注册显示。 此设置与其他三个命令不同。 若要控制显示哪些寄存器和标志，请使用 [**rm (注册掩码)**](rm--register-mask-.md) 命令。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span>*StartAddress*   
指定调试器开始执行的地址。 否则，调试器会从指令指针指向的指令开始。 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span>*计数*   
指定在此命令停止时必须遇到的 **返回** 指令的数目。 默认值为一。

<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span>*命令*   
指定执行步骤之后要执行的调试器命令。 此命令在显示标准 **pt** 结果之前执行。 如果还使用 *Count*，则指定的命令将在所有单步完成之后执行， (但在最后一步的结果显示) 之前。

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
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令的详细信息，请参阅 [控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

**Pt** 命令导致目标开始执行。 此执行将继续，直到到达 **返回** 指令或遇到断点。

如果程序计数器已在 **返回** 指令上，则执行整个返回。 返回此返回后，将继续执行，直到到达另一个 **返回** 。 这种执行（而非跟踪）是在 **pt** 和 [**tt (Trace 之间唯一不同于下一个返回)**](tt--trace-to-next-return-.md)。

在源模式下，可以将一个源行与多个程序集指令相关联。 **Pt** 命令不会在与当前源行关联的 **返回** 指令处停止。

下面的示例演示如何结合使用 **pt** 命令和 **kb** 命令来显示堆栈跟踪：

```dbgcmd
0:000> pt "kb"
```

 

 





