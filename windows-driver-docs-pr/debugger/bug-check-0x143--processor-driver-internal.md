---
title: Bug 检查 0x143 PROCESSOR_DRIVER_INTERNAL
description: PROCESSOR_DRIVER_INTERNAL bug 检查的值为0x00000143。 这表明处理器电源管理 (PPM) 驱动程序遇到错误。
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
ms.openlocfilehash: 9637a2ea19da32edcc370490072a2600573680e9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824291"
---
# <a name="bug-check-0x143-processor_driver_internal"></a>Bug 检查0x143： \_ 内部处理器驱动程序 \_


处理器 \_ 驱动程序 \_ 内部 bug 检查的值为0x00000143。 这表明处理器电源管理 (PPM) 驱动程序遇到错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="processor_driver_internal-parameters"></a>处理器 \_ 驱动程序 \_ 内部参数


| 参数 | 描述                                                              |
|-----------|--------------------------------------------------------------------------|
| 1         | 1-Power Engine 插件 (PEP) 无法接受所需的通知    |
| 2         | PEP 运行时通知类型                                            |
| 3         | 指向通知消息的指针                                          |
| 4         | 指向处理器设备上下文的指针 (\_ 发出通知) FDO 数据 |

 

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
<td align="left">2-Power Engine 插件 (PEP) 返回无效处理器空闲状态</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left"><p>无效状态的类型</p>
<p>0x0： PEP 请求的处理器太多，无法协调空闲状态</p>
参数 3-请求参与协调空闲转换的处理器数参数 4-指向处理器设备上下文的指针 (FDO_DATA) 
<p>0x1： PEP 请求的处理器处于无效空闲状态</p>
参数 3-空闲状态索引请求的参数 4-指向处理器设备上下文的指针 (与无效空闲状态相对应的 FDO_DATA) 
<p>0x2： PEP 请求平台处于无效的空闲状态</p>
参数 3-平台空闲状态索引请求的参数 4-指向处理器设备上下文的指针 (与无效空闲状态相对应的 FDO_DATA) </td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">请参阅参数2</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">请参阅参数2</td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

处理器驱动程序检测到 irreconcilable 条件，这会提示它进行错误检查。 在处理器空闲和性能状态更改执行期间可能会发生这种情况，这可能涉及到其他实体，例如内核、HAL 和 Power Engine 插件)  (PEP。 来自错误检查的信息将帮助识别处理器驱动程序在处理其他实体时所做的假设。 根本原因可能是其他实体中的，转储文件可能会显示详细信息以确定错误检查的原因。

 

 




