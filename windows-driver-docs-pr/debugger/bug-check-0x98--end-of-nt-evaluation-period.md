---
title: Bug 检查 0x98 END_OF_NT_EVALUATION_PERIOD
description: END_OF_NT_EVALUATION_PERIOD bug 检查的值为0x00000098。 此 bug 检查表明 Microsoft Windows 操作系统的试用期已结束。
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
ms.openlocfilehash: f33cfd8309615006190121babdcb770772f6d7a9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840447"
---
# <a name="bug-check-0x98-end_of_nt_evaluation_period"></a>Bug 检查0x98： \_ \_ NT \_ 评估 \_ 期结束


\_ \_ NT \_ 评估 \_ 期 bug 检查结束时，值为0x00000098。 此 bug 检查表明 Microsoft Windows 操作系统的试用期已结束。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="end_of_nt_evaluation_period-parameters"></a>\_ \_ NT \_ 评估 \_ 期参数结束


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
<td align="left"><p>产品到期日期的低序位32位</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>产品到期日期的高序位32位</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

Windows 操作系统的安装是一个具有到期日期的评估单元。 试用期已结束。

 

 




