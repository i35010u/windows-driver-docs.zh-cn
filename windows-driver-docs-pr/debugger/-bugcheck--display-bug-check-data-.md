---
title: .bugcheck（显示 Bug 检查数据）
description: .Bugcheck 命令显示在目标计算机上的 bug 检查中的数据。
ms.assetid: 4b453b5a-4a3c-4056-92e7-b6a17f987fa4
keywords:
- .bugcheck （显示 Bug 检查数据） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .bugcheck (Display Bug Check Data)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a24198184af88054b599c230d8e308bdd3d882fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336934"
---
# <a name="bugcheck-display-bug-check-data"></a>.bugcheck（显示 Bug 检查数据）


**.Bugcheck**命令显示来自错误数据时，请在目标计算机。

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
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式下</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关错误检查的详细信息，请参阅[Bug 检查 （蓝屏）](bug-checks--blue-screens-.md)。 单个错误检查的说明，请参阅[Bug 检查代码参考](bug-check-code-reference2.md)部分。

<a name="remarks"></a>备注
-------

此命令显示当前的 bug 检查数据。 （此 bug 检查数据将可访问的崩溃的计算机重启。）

您还可以显示 bug 检查数据在 32 位系统上使用**dd NT ！KiBugCheckData L5**，或通过使用 64 位系统上**dq NT ！KiBugCheckData L5**。 但是，.bugcheck 命令是更加可靠，因为它在某些情况下， [ **d\* （显示内存）** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令将不 （如用户模式的小型转储）。

[ **！ 分析**](-analyze.md)的 bug 检查发生后，扩展命令也是很有用。

 

 





