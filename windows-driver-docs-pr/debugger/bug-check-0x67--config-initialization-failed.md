---
title: Bug 检查 0x67 CONFIG_INITIALIZATION_FAILED
description: CONFIG_INITIALIZATION_FAILED bug 检查具有 0x00000067 值。 检查此错误表示注册表配置失败。
ms.assetid: 3bc4d6d9-785e-4283-b4c5-2c868c03f084
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
ms.openlocfilehash: d075b54a054a7a5788befce178a757cea594475a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363149"
---
# <a name="bug-check-0x67-configinitializationfailed"></a>Bug 检查 0x67：CONFIG\_初始化\_失败


在配置\_初始化\_失败错误检查的值为 0x00000067。 检查此错误表示注册表配置失败。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="configinitializationfailed-parameters"></a>CONFIG\_初始化\_失败参数


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
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

注册表无法分配包含注册表文件所需的池。 这种情况下应永远不会发生，因为寄存器分配尽可能早地在系统初始化此池，以便在很多页面缓冲池应可用。

 

 




