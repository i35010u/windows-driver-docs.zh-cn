---
title: 启用堆释放检查
description: 启用堆释放检查
keywords:
- " (全局标志启用堆免费检查) "
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2e3d0283cdeb4765dcd82cba4a3cca9ed5f8710
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834753"
---
# <a name="enable-heap-free-checking"></a>启用堆释放检查


## <span id="ddk_enable_heap_free_checking_dtools"></span><span id="DDK_ENABLE_HEAP_FREE_CHECKING_DTOOLS"></span>


**启用堆自由检查** 标志会在释放每个堆分配后对其进行验证。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>hfc</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x20</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_HEAP_ENABLE_FREE_CHECK</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围的注册表项、内核标志、映像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idsee_alsospanspan-idsee_alsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>另请参阅

[启用堆结尾检查](enable-heap-tail-checking.md)， [启用堆参数检查](enable-heap-parameter-checking.md)

 

 





