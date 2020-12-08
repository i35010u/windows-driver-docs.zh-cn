---
title: Bug 检查 0x12F VHD_BOOT_INITIALIZATION_FAILED
description: VHD_BOOT_INITIALIZATION_FAILED bug 检查的值为0x0000012F。 这表明尝试从 VHD 启动时出现初始化失败。
keywords:
- Bug 检查 0x12F VHD_BOOT_INITIALIZATION_FAILED
- VHD_BOOT_INITIALIZATION_FAILED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VHD_BOOT_INITIALIZATION_FAILED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7939d6870dd3e828e3d9d53e5b53b643dc4dd022
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826941"
---
# <a name="bug-check-0x12f-vhd_boot_initialization_failed"></a>Bug 检查0x12F： VHD \_ 启动 \_ 初始化 \_ 失败


VHD \_ 启动 \_ 初始化 \_ 失败 bug 检查的值为0x0000012F。 这表明尝试从 VHD 启动时出现初始化失败。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="vhd_boot_initialization_failed-parameters"></a>VHD \_ 启动 \_ 初始化 \_ 失败参数


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
<td align="left"><p>失败的操作</p>
1：无法从启动设备提取 VHD 信息。
2：等待 VHD 父设备到表面的超时。
3： VHD 路径字符串内存分配错误。
4： VHD 路径构造失败。
5： VHD 启动设备装载失败。
6：禁用睡眠状态失败。
7： VHD 信息内存分配错误。
8： VHD 信息构造失败。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">NT 状态代码</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">预留</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">预留</td>
</tr>
</tbody>
</table>

 

 

 




