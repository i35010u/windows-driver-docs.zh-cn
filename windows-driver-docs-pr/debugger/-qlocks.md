---
title: qlocks
description: Qlocks 扩展显示的所有排队的自旋锁的状态。
ms.assetid: fdeefedb-c840-410a-94e4-ae42923e82e7
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
ms.openlocfilehash: 475431764925dd6e584f9099173963c23c505c53
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334330"
---
# <a name="qlocks"></a>!qlocks


**！ Qlocks**扩展显示的所有排队的自旋锁的状态。

```dbgcmd
!qlocks 
```

## <span id="ddk__qlocks_dbg"></span><span id="DDK__QLOCKS_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

数值调节钮的锁有关的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。

<a name="remarks"></a>备注
-------

此命令将仅在多处理器系统上很有用。

下面是一个示例：

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

 

 





