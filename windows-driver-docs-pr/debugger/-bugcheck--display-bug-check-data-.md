---
title: .bugcheck（显示 Bug 检查数据）
description: 错误检查命令显示目标计算机上 bug 检查中的数据。
keywords:
- ) Windows 调试，检查 (显示 Bug 检查数据
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .bugcheck (Display Bug Check Data)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0d2ebfa5d637543012273c281e3bb97120145bd7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814131"
---
# <a name="bugcheck-display-bug-check-data"></a>.bugcheck（显示 Bug 检查数据）


**错误** 检查命令显示目标计算机上 bug 检查中的数据。

```dbgsyntax
    .bugcheck 
```

## <span id="ddk_meta_display_bug_check_data_dbg"></span><span id="DDK_META_DISPLAY_BUG_CHECK_DATA_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅限内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 bug 检查的详细信息，请参阅 [Bug 检查 (蓝屏) ](bug-checks--blue-screens-.md)。 有关各个 bug 检查的说明，请参阅 [Bug 检查代码参考](bug-check-code-reference2.md) 部分。

<a name="remarks"></a>备注
-------

此命令显示当前 bug 检查数据。  (此错误检查数据将可访问，直到重新启动崩溃的计算机。 ) 

你还可以使用 dd NT 在32位系统上显示 bug 检查数据 **！KiBugCheckData L5**，或在64位系统上使用 **dq NT！KiBugCheckData L5**。 但是，错误检查命令更可靠，因为在 [**d \* (显示) 内存**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md) 的某些情况下，该命令将不 (如用户模式小型转储) 。

发生 bug 检查后，" [**！分析**](-analyze.md) 扩展" 命令也很有用。

 

 





