---
title: tp
description: Tp 扩展显示线程池信息。
keywords:
- 线程池
- tp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- tp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fa36c33d6f614095a3d5082833177e02540c2508
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819925"
---
# <a name="tp"></a>!tp


**！ Tp** 扩展显示线程池信息。

```dbgcmd
!tp pool Address [Flags] 
!tp tqueue Address [Flags] 
!tp ItemType Address [Flags] 
!tp ThreadType [Address] 
!tp stats Address [Flags] 
!tp wfac Address 
!tp wqueue Address Priority Node 
!tp -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______pool_Address_____________"></span><span id="_______pool_address_____________"></span><span id="_______POOL_ADDRESS_____________"></span>**池**  **** *地址*   
导致显示整个线程池的 *地址* 。 如果 *Address* 为0，则将显示所有线程池。

<span id="_______tqueue_______Address______"></span><span id="_______tqueue_______address______"></span><span id="_______TQUEUE_______ADDRESS______"></span>**t**  **** *地址*   
导致显示位于 *地址* 的活动计时器队列。

<span id="_______ItemType_Address______"></span><span id="_______itemtype_address______"></span><span id="_______ITEMTYPE_ADDRESS______"></span>*ItemType 地址*   
导致显示指定的线程池项。 *Address* 指定项的地址。 *ItemType* 指定项的类型;这可能包括以下任何一种可能性：

<span id="obj"></span><span id="OBJ"></span>**obj**  
将显示一个 (例如 IO 项) 的通用池项。

<span id="timer"></span><span id="TIMER"></span>**记**  
将显示计时器项。

<span id="wait"></span><span id="WAIT"></span>**再**  
将显示一个等待项。

<span id="work"></span><span id="WORK"></span>**解决**  
将显示一个工作项。

<span id="_______ThreadType__Address_"></span><span id="_______threadtype__address_"></span><span id="_______THREADTYPE__ADDRESS_"></span>*ThreadType* \[*地址*\]  
导致显示指定类型的线程。 如果包含 *地址* 且非零，则仅显示此地址的线程。 如果 *Address* 为0，则显示与 *ThreadType* 匹配的所有线程。 如果省略 *Address* ，则只显示与当前线程关联的 *ThreadType* 匹配的线程。 *ThreadType* 指定要显示的线程的类型;这可能包括以下任何一种可能性：

<span id="waiter"></span><span id="WAITER"></span>**阻塞**  
将显示线程池等待线程。

<span id="worker"></span><span id="WORKER"></span>**工人**  
将显示一个线程池工作线程。

<span id="stats__Address_"></span><span id="stats__address_"></span><span id="STATS__ADDRESS_"></span>**统计** **\[** 信息 <em>地址</em>**\]**  
导致显示当前线程的调试统计信息。 *地址* 可以省略，但如果指定，则它必须等于-1 (负一) ，以表示当前线程。

<span id="_______wfac_______Address______"></span><span id="_______wfac_______address______"></span><span id="_______WFAC_______ADDRESS______"></span>**wfac**  **** *地址*   
 (Windows 7 和更高版本仅) 会导致显示辅助进程工厂 *地址* 。 指定的 *地址* 必须是有效的非零地址。

<span id="_______wqueue_______Address______"></span><span id="_______wqueue_______address______"></span><span id="_______WQUEUE_______ADDRESS______"></span>**wqueue**  **** *地址*   
 (Windows 7 和更高版本仅) 会导致显示工作队列和 NUMA 节点 matche 以下内容：指定的优先级、指定的 NUMA 节点，以及 NUMA 节点所属的指定地址的池。 *Address* 指定池的地址。 使用 **wqueue** 参数时，该参数必须后接 " *Address*"、" *Priority*" 和 " *Node*"。

<span id="_______Priority______"></span><span id="_______priority______"></span><span id="_______PRIORITY______"></span>*优先级*   
 (Windows 7 和更高版本仅) 指定要显示的工作队列的优先级别。 *优先级* 可以是以下任一值：

<span id="0"></span>**0**  
显示具有高优先级的工作队列。

<span id="1"></span>**1**  
显示具有普通优先级的工作队列。

<span id="2"></span>**pps-2**  
显示低优先级的工作队列。

<span id="-1"></span>**-1**  
显示所有工作队列。

<span id="_______Node______"></span><span id="_______node______"></span><span id="_______NODE______"></span>*节点*   
 (Windows 7 和更高版本仅) 指定属于由 *Address* 指定的池的 NUMA 节点。 如果 *Node* 为-1 (为) ，则显示所有 NUMA 节点。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定显示内容应包含的内容。 这可以是以下任一位值的总和 (默认值为 0x0) ：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
使显示为单行输出。 显示 *ItemType* 时，此位值对输出没有影响。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
使显示内容包含成员信息。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)   
仅当使用 **pool** 选项时，此标志才适用。 在 Windows XP、Windows Server 2003、Windows Vista 和 Windows Server 2008 中，此标志将导致显示包含池工作队列。 在 Windows 7 和更高版本中，此标志将导致显示的所有池工作队列都处于正常优先级和所有 NUMA 节点。

<span id="_______-_______"></span> **-?**   
在调试器中显示此扩展的简短帮助文本命令窗口。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关线程池的信息，请参阅 Microsoft Windows SDK 文档。

 

 





