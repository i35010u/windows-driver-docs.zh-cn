---
title: 后备链
description: 后备链扩展显示有关视列表的信息，将视列表的计数器重置或修改视列表的深度。
ms.assetid: ec343563-f293-4ddf-96c8-69fc7b9b4377
keywords:
- 后备链列表
- 后备链 Windows 调试
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
ms.openlocfilehash: a94732fc070f29d09aa343e8ad31f54fe53af299
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365791"
---
# <a name="lookaside"></a>!lookaside


**！ 后备链**扩展显示有关视列表的信息、 将视列表的计数器重置或修改视列表的深度。

```dbgcmd
!lookaside [Address [Options [Depth]]]
!lookaside [-all]
!lookaside 0 [-all]
```

## <a name="span-idddklookasidedbgspanspan-idddklookasidedbgspanparameters"></a><span id="ddk__lookaside_dbg"></span><span id="DDK__LOOKASIDE_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定要显示或修改视列表的十六进制的地址。

如果*地址*省略 （或 0） 和 **-所有**未指定选项，将显示一组已知的标准系统视列表。 组列表并不详尽;也就是说，它不包括所有系统视列表。 此外，一组不包括通过调用创建的自定义视列表[ **ExInitializePagedLookasideList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializepagedlookasidelist)或[ **ExInitializeNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializenpagedlookasidelist).

如果*地址*省略 （或 0） 和 **-所有**指定选项，将显示所有视列表。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
控制将执行哪些操作。 以下可能*选项*支持。 默认值为零：

<span id="0"></span>0  
显示有关指定的备用列表或列表的信息。

<span id="1"></span>1  
重置指定的备用列表的计数器。

<span id="2"></span>2  
修改指定的备用列表的深度。 可以仅使用此选项，如果*地址*为非零值。

<span id="_______Depth______"></span><span id="_______depth______"></span><span id="_______DEPTH______"></span> *深度*   
指定新的指定的备用列表的最大深度。 此参数允许才*地址*为非零值和*选项*等于 2。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关视列表的信息，请参阅[Windows Driver Kit (WDK) 文档](https://go.microsoft.com/fwlink/p/?linkid=201141)并*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

视列表是包含多个处理器安全机制，用于管理从分页或非分页内存池的大小固定的项。

视列表都高效，因为例程不在大多数平台上使用自旋锁。

请注意，如果视列表的当前深度超过了该列表中，然后释放与该列表相关联的结构的最大深度将会导致释放到池的内存，而不是列出内存。

下面是输出的来自此扩展插件示例：

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
<td align="left">Kdexts.dll</td>
</tr>
</tbody>
</table>

 

 





