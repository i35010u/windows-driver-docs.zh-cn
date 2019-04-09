---
title: Bug 检查 0x98 END_OF_NT_EVALUATION_PERIOD
description: END_OF_NT_EVALUATION_PERIOD bug 检查具有 0x00000098 值。 此 bug 检查指示 Microsoft Windows 操作系统的试用期已结束。
ms.assetid: e49ea686-27b9-4743-9339-766b4748e29b
keywords:
- Bug 检查 0x98 END_OF_NT_EVALUATION_PERIOD
- END_OF_NT_EVALUATION_PERIOD
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- END_OF_NT_EVALUATION_PERIOD
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 564fe7b775c33150bdca8005870c18936abdb2f6
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239146"
---
# <a name="bug-check-0x98-endofntevaluationperiod"></a>Bug 检查 0x98：结束\_OF\_NT\_评估\_段


结束\_OF\_NT\_评估\_时间段的 bug 检查的值为 0x00000098。 此 bug 检查指示 Microsoft Windows 操作系统的试用期已结束。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="endofntevaluationperiod-parameters"></a>结束\_OF\_NT\_评估\_PERIOD 参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>个产品到期日期的低 32 位</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>个产品到期日期的高 32 位</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

安装 Windows 操作系统的是带有到期日期的计算单元。 试用期限已结束。

 

 




