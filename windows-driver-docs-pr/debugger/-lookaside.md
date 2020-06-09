---
title: 后备链表
description: 后备链表扩展显示有关 "搁置" 列表的信息、重置 "搁置" 列表的计数器或修改 "查找" 列表的深度。
ms.assetid: ec343563-f293-4ddf-96c8-69fc7b9b4377
keywords:
- 后备链表列表
- 后备链表 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lookaside
api_location:
- Kdexts.dll
api_type:
- DllExport
ms.localizationpriority: medium
ms.openlocfilehash: 0258a15ffc796429500bb8e95e5ad1d0f3958f3a
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534742"
---
# <a name="lookaside"></a>!lookaside


**！后备链表**extension 显示有关 "搁置" 列表的信息、重置 "搁置" 列表的计数器或修改 "查找" 列表的深度。

```dbgcmd
!lookaside [Address [Options [Depth]]]
!lookaside [-all]
!lookaside 0 [-all]
```

## <a name="span-idddk__lookaside_dbgspanspan-idddk__lookaside_dbgspanparameters"></a><span id="ddk__lookaside_dbg"></span><span id="DDK__LOOKASIDE_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要显示或修改的外观列表的十六进制地址。

如果省略了*Address* （或0），并且未指定 **-all**选项，则会显示一组众所周知的标准系统的 "查找" 列表。 列表集并非详尽;也就是说，它不包含所有系统旁的列表。 此外，该集不包含通过调用[**ExInitializePagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializepagedlookasidelist)或[**ExInitializeNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializenpagedlookasidelist)创建的自定义外观列表。

如果省略了*Address* （或0），并且指定了 **-all**选项，则会显示所有的查找列表。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
控制要执行的操作。 支持以下可能*选项*。 默认值为零：

<span id="0"></span>0  
显示有关指定的外观列表的信息。

<span id="1"></span>1  
重置指定的查找列表的计数器。

<span id="2"></span>2  
修改指定的外观列表的深度。 仅当*Address*为非零值时，才可以使用此选项。

<span id="_______Depth______"></span><span id="_______depth______"></span><span id="_______DEPTH______"></span>*深度*   
指定指定外观列表的新的最大深度。 仅当*Address*为非零且*Options*等于2时，才允许使用此参数。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 "查找" 列表的信息，请参阅[使用后备链表列表](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-lookaside-lists)和*Microsoft Windows 内部机制*，并将其标记为 Russinovich 和 David

<a name="remarks"></a>备注
-------

"查找" 列表是多处理器安全机制，用于在分页或非分页内存中管理固定大小的条目池。

看起来很有效，因为例程在大多数平台上不使用自旋锁。

请注意，如果现有的现有深度列表超出了该列表的最大深度，则释放与该列表关联的结构将导致将其释放到池内存，而不是列出内存。

下面是此扩展的输出示例：

```dbgcmd
!lookaside 0xfffff88001294f80

Lookaside "" @ 0xfffff88001294f80  Tag(hex): 0x7366744e "Ntfs"
    Type           =       0011  PagedPool RaiseIfAllocationFailure
    Current Depth  =          0  Max Depth  =          4
    Size           =        496  Max Alloc  =       1984
    AllocateMisses =          8  FreeMisses =          0
    TotalAllocates =     272492  TotalFrees =     272488
    Hit Rate       =         99% Hit Rate   =        100%
```

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">Kdexts</td>
</tr>
</tbody>
</table>

 

 





