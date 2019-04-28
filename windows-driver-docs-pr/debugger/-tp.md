---
title: tp
description: Tp 扩展显示线程池的信息。
ms.assetid: 33b22e04-b781-4890-8142-c2624fdc4055
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
ms.openlocfilehash: 9a8a69493a7dc793784e5ac1cd56adb231258e46
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334190"
---
# <a name="tp"></a>!tp


**！ Tp**扩展显示线程池的信息。

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

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______pool_Address_____________"></span><span id="_______pool_address_____________"></span><span id="_______POOL_ADDRESS_____________"></span> **pool** **** *Address*   
导致在整个线程池中*地址*显示。 如果*地址*为 0，则将显示所有线程池。

<span id="_______tqueue_______Address______"></span><span id="_______tqueue_______address______"></span><span id="_______TQUEUE_______ADDRESS______"></span> **tqueue** **** *Address*   
导致在活动计时器队列*地址*显示。

<span id="_______ItemType_Address______"></span><span id="_______itemtype_address______"></span><span id="_______ITEMTYPE_ADDRESS______"></span> *ItemType Address*   
使指定的线程池项来显示。 *地址*指定项的地址。 *ItemType*指定类型的项; 这可以包含任何以下可能性：

<span id="obj"></span><span id="OBJ"></span>**obj**  
将显示通用池项 （例如 IO 的项）。

<span id="timer"></span><span id="TIMER"></span>**timer**  
将显示计时器项。

<span id="wait"></span><span id="WAIT"></span>**wait**  
将显示等待项。

<span id="work"></span><span id="WORK"></span>**work**  
将显示工作项。

<span id="_______ThreadType__Address_"></span><span id="_______threadtype__address_"></span><span id="_______THREADTYPE__ADDRESS_"></span> *ThreadType* \[*Address*\]  
导致要显示的指定类型的线程。 如果*地址*包含和非零值，则只有在此地址的线程才会显示。 如果*地址*为 0，匹配的所有线程*ThreadType*显示。 如果*地址*省略，则仅匹配的线程*ThreadType*关联与当前线程会显示。 *ThreadType*指定类型的线程显示; 这可以包含任何以下可能性：

<span id="waiter"></span><span id="WAITER"></span>**waiter**  
将显示一个线程池等待应用程序线程。

<span id="worker"></span><span id="WORKER"></span>**worker**  
将显示线程池工作线程。

<span id="stats__Address_"></span><span id="stats__address_"></span><span id="STATS__ADDRESS_"></span>**stats** **\[**<em>Address</em>**\]**  
将导致当前线程用来显示调试统计信息。 *地址*可能被忽略，但如果指定了它，则它必须等于-1 (1)，以表示当前线程。

<span id="_______wfac_______Address______"></span><span id="_______wfac_______address______"></span><span id="_______WFAC_______ADDRESS______"></span> **wfac** **** *Address*   
(Windows 7 及更高版本)导致在辅助角色工厂*地址*显示。 指定*地址*必须是有效的非零地址。

<span id="_______wqueue_______Address______"></span><span id="_______wqueue_______address______"></span><span id="_______WQUEUE_______ADDRESS______"></span> **wqueue** **** *Address*   
(Windows 7 及更高版本)导致该匹配出现以下的工作队列和 NUMA 节点的显示： 指定的优先级、 指定的 NUMA 节点和池，在指定的地址，属于的 NUMA 节点。 *地址*指定池的地址。 当**wqueue**参数，它的后面必须跟*地址*，*优先级*，以及*节点*。

<span id="_______Priority______"></span><span id="_______priority______"></span><span id="_______PRIORITY______"></span> *优先级*   
(Windows 7 及更高版本)指定要显示的工作队列的优先级级别。 *优先级*可以是任何以下值：

<span id="0"></span>**0**  
显示具有高优先级的工作队列。

<span id="1"></span>**1**  
显示以正常优先级的工作队列。

<span id="2"></span>**2**  
显示以低优先级的工作队列。

<span id="-1"></span>**-1**  
显示所有工作队列。

<span id="_______Node______"></span><span id="_______node______"></span><span id="_______NODE______"></span> *Node*   
(Windows 7 及更高版本)指定属于该池指定的一个 NUMA 节点*地址*。 如果*节点*为-1 (1)，显示所有的 NUMA 节点。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定显示应包含的内容。 这可以是任何以下 （默认值为 0x0） 的位值的总和：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
将导致显示的单行输出。 此位值不起作用的输出时*ItemType*显示。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
将导致显示以包括成员信息。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
此标志是唯一时才可用**池**使用选项。 在 Windows XP、 Windows Server 2003，Windows Vista 和 Windows Server 2008 中，此标记会显示以包括池工作队列。 在 Windows 7 和更高版本，此标记会显示以包括在普通优先级的所有池的工作队列和所有 NUMA 节点。

<span id="_______-_______"></span> **-?**   
在调试器命令窗口中显示此扩展的简短帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关线程池的信息，请参阅 Microsoft Windows SDK 文档。

 

 





