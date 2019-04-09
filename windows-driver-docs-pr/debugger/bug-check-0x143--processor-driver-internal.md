---
title: Bug 检查 0x143 PROCESSOR_DRIVER_INTERNAL
description: PROCESSOR_DRIVER_INTERNAL bug 检查具有 0x00000143 值。 这表示处理器电源管理 (PPM) 驱动程序遇到错误。
ms.assetid: B61A1DF1-4454-4418-866F-FD9EC96F6906
keywords:
- Bug 检查 0x143 PROCESSOR_DRIVER_INTERNAL
- PROCESSOR_DRIVER_INTERNAL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PROCESSOR_DRIVER_INTERNAL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1766f98e3ba794c439ab187d494a7719e8525ea7
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238476"
---
# <a name="bug-check-0x143-processordriverinternal"></a>Bug 检查 0x143：处理器\_驱动程序\_内部


处理器\_驱动程序\_内部 bug 检查的值为 0x00000143。 这表示处理器电源管理 (PPM) 驱动程序遇到错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="processordriverinternal-parameters"></a>处理器\_驱动程序\_内部参数


| 参数 | 描述                                                              |
|-----------|--------------------------------------------------------------------------|
| 1         | 1-power 引擎 Plugin(PEP) 无法接受所需的通知    |
| 2         | PEP 运行时通知类型                                            |
| 3         | 指向通知消息                                          |
| 4         | 到处理器的设备上下文的指针 (FDO\_数据) 发出通知 |

 

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
<td align="left">1</td>
<td align="left">2-power 引擎插件 (PEP) 返回了无效的处理器空闲的状态</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left"><p>类型的无效状态</p>
<p>0x0:PEP 请求过多处理器，用于协调空闲状态</p>
参数 3 的处理器数请求指向处理器设备上下文 (FDO_DATA) 的参与协调空闲转换参数 4-
<p>0x1:PEP 请求的处理器处于空闲状态无效</p>
参数 3 的空闲状态索引请求参数 4-指向无效的空闲状态所对应的处理器的设备上下文 (FDO_DATA)
<p>0x2:PEP 请求处于空闲状态无效的平台</p>
参数 3-平台空闲状态索引请求参数 4-指向无效的空闲状态所对应的处理器的设备上下文 (FDO_DATA)</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">引用参数 2</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">引用参数 2</td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

处理器驱动程序检测到的提示错误检测到的不可调和条件。 这可能会发生期间处理器空闲和性能状态更改执行，这可能涉及其他此类的实体具有内核，HAL 和引擎插件 (PEP)。 从检测错误的信息将帮助您识别违反了其处理其他实体中的处理器驱动程序所做的假设。 在其他实体中可能存在的根本原因和转储文件可能会泄漏来确定检测的错误的原因的详细信息。

 

 




