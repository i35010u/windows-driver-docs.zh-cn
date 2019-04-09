---
title: Bug 检查 0x12F VHD_BOOT_INITIALIZATION_FAILED
description: VHD_BOOT_INITIALIZATION_FAILED bug 检查具有 0x0000012F 值。 这表示初始化失败尝试从 VHD 启动时出现。
ms.assetid: CC4CD97B-FCBA-4B73-AB9E-D56387D4CB07
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
ms.openlocfilehash: c246608a047249419203a3e7275f2dbba41c4895
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238387"
---
# <a name="bug-check-0x12f-vhdbootinitializationfailed"></a>Bug 检查 0x12F：VHD\_引导\_初始化\_失败


VHD\_引导\_初始化\_失败错误检查的值为 0x0000012F。 这表示初始化失败尝试从 VHD 启动时出现。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="vhdbootinitializationfailed-parameters"></a>VHD\_引导\_初始化\_失败参数


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
1 :无法提取 VHD 信息从启动设备。
2 :正在等待到图面的 VHD 父设备超时。
3 :VHD 路径字符串内存分配错误。
4 :VHD 路径构造失败。
5 :VHD 引导设备装入失败。
6 :禁用睡眠状态失败。
7 :VHD 信息内存分配错误。
8 :VHD 的信息构造失败。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">NT 状态代码</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">保留</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">保留</td>
</tr>
</tbody>
</table>

 

 

 




