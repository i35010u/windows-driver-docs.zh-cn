---
title: Bug 检查 0x67 CONFIG_INITIALIZATION_FAILED
description: CONFIG_INITIALIZATION_FAILED bug 检查的值为0x00000067。 此 bug 检查表明注册表配置失败。
keywords:
- Bug 检查 0x67 CONFIG_INITIALIZATION_FAILED
- CONFIG_INITIALIZATION_FAILED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CONFIG_INITIALIZATION_FAILED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 94efdf8d7ab4c9db0cf88a76da4950f2ff6238e1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838683"
---
# <a name="bug-check-0x67-config_initialization_failed"></a>Bug 检查0x67：配置 \_ 初始化 \_ 失败


配置 \_ 初始化 \_ 失败 bug 检查的值为0x00000067。 此 bug 检查表明注册表配置失败。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="config_initialization_failed-parameters"></a>配置 \_ 初始化 \_ 失败参数


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
<td align="left"><p>位置选择器</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>NT 状态代码</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

注册表无法分配包含注册表文件所需的池。 永远不会发生这种情况，因为在系统初始化中，寄存器会提前分配此池，以便有充足的分页池可用。

 

 




