---
title: qlocks
description: Qlocks 扩展显示所有排队自旋锁的状态。
keywords:
- qlocks Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- qlocks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2b81387b7d3b68a59c96dabda38041c36992fda8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837587"
---
# <a name="qlocks"></a>!qlocks


**！ Qlocks** 扩展显示所有排队的自旋锁的状态。

```dbgcmd
!qlocks 
```

## <span id="ddk__qlocks_dbg"></span><span id="DDK__QLOCKS_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关自旋锁的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部*，并将其标记为 Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

此命令仅在多处理器系统上有用。

以下是示例：

```dbgcmd
0: kd> !qlocks
Key: O = Owner, 1-n = Wait order, blank = not owned/waiting, C = Corrupt

                       Processor Number
    Lock Name         0  1  2  3

KE   - Dispatcher               
KE   - Unused Spare             
MM   - PFN                      
MM   - System Space             
CC   - Vacb                     
CC   - Master                   
EX   - NonPagedPool             
IO   - Cancel                   
EX   - WorkQueue                
IO   - Vpb                      
IO   - Database                 
IO   - Completion               
NTFS - Struct                   
AFD  - WorkQueue                
CC   - Bcb                      
MM   - MM NonPagedPool             
```

 

 





