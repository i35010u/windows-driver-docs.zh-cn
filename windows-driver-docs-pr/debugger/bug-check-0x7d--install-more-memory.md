---
title: Bug 检查 0x7D INSTALL_MORE_MEMORY
description: INSTALL_MORE_MEMORY bug 检查的值为0x0000007D。 此 bug 检查表明没有足够的内存来启动 Microsoft Windows 操作系统。
keywords:
- Bug 检查 0x7D INSTALL_MORE_MEMORY
- INSTALL_MORE_MEMORY
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INSTALL_MORE_MEMORY
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c23412a30f6fb94426b8308f8cf28aafbcee110c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840845"
---
# <a name="bug-check-0x7d-install_more_memory"></a>Bug 检查0x7D：安装 \_ 更多 \_ 内存


"安装 \_ 更多 \_ 内存 bug 检查" 的值为 "0x0000007D"。 此 bug 检查表明没有足够的内存来启动 Microsoft Windows 操作系统。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="install_more_memory-parameters"></a>安装 \_ 更多 \_ 内存参数


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
<td align="left"><p>找到的物理页数</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>最低物理页面</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>最高物理页面</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

Windows 操作系统没有足够的内存来完成启动过程。

<a name="resolution"></a>解决方法
----------

安装更多内存。

 

 




