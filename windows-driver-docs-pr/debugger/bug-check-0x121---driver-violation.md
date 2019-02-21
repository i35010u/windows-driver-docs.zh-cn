---
title: Bug 检查 0x121 DRIVER_VIOLATION
description: DRIVER_VIOLATION bug 检查具有 0x00000121 值。 此 bug 检查指示驱动程序导致冲突。
ms.assetid: 4a5d1d84-a958-45a6-9511-b5b4ecd4c067
keywords:
- Bug 检查 0x121 DRIVER_VIOLATION
- DRIVER_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2142a6e5724ccfd48f1a94aa0f923a38b1c662b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534537"
---
# <a name="bug-check-0x121-driverviolation"></a>Bug 检查 0x121:驱动程序\_冲突


该驱动程序\_冲突错误检查的值为 0x00000121。 此 bug 检查指示驱动程序导致冲突。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="driverviolation-parameters"></a>驱动程序\_冲突参数


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
<td align="left"><p>描述冲突的类型</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

使用内核调试程序并查看调用堆栈，以确定引起冲突的驱动程序的名称： [ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息，可以是非常有帮助在确定根本原因，然后输入之一[ **k （显示堆栈回溯）** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-)命令以查看调用堆栈。

 

 




