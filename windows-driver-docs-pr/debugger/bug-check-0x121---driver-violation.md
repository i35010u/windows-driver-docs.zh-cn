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
ms.openlocfilehash: 8e80b189a39ae5b36bd7ee713e47886cff963904
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520838"
---
# <a name="bug-check-0x121-driverviolation"></a>Bug 检查 0x121：驱动程序\_冲突


该驱动程序\_冲突错误检查的值为 0x00000121。 此 bug 检查指示驱动程序导致冲突。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


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

使用内核调试程序并查看调用堆栈，以确定引起冲突的驱动程序的名称： [ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息，有助于在确定根本原因，然后输入之一[ **k （显示堆栈回溯）** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-)命令以查看调用堆栈。

 

 




