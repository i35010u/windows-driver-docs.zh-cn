---
title: Bug 检查 0x51 REGISTRY_ERROR
description: REGISTRY_ERROR bug 检查具有 0x00000051 值。 这表示出现严重注册表错误。
ms.assetid: 286e462f-e4d4-408f-91ad-3e20336e2025
keywords:
- Bug 检查 0x51 REGISTRY_ERROR
- REGISTRY_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- REGISTRY_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 34c5eefebaadadc76b09dcb784d8b280e9e192bd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367413"
---
# <a name="bug-check-0x51-registryerror"></a>Bug 检查 0x51：注册表\_错误


注册表\_错误 bug 检查的值为 0x00000051。 这表示出现严重注册表错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="registryerror-parameters"></a>注册表\_错误参数


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
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>指向该配置单元 （如果可用） 的指针</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>如果该配置单元已损坏，返回代码<strong>HvCheckHive</strong> （如果可用）</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

出现了问题的注册表。 如果可用的内核调试程序，获得堆栈跟踪： [ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示 bug 检查有关的信息和可以确定根本原因，很有帮助，然后输入之一[ **k （显示堆栈回溯）** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-)命令以查看调用堆栈。

此错误可能表示注册表尝试读取的一个文件时遇到 I/O 错误。 原因可能是由硬件问题或文件系统损坏。

它还会由于在刷新操作中，仅在使用安全系统，该故障可能会出现，然后仅当资源限制遇到。

 

 




