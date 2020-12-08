---
title: Bug 检查 0x12A MUI_NO_VALID_SYSTEM_LANGUAGE
description: MUI_NO_VALID_SYSTEM_LANGUAGE bug 检查的值为0x0000012A。 这表明 Windows 找不到任何已安装的许可语言包（系统默认 UI 语言）。
keywords:
- Bug 检查 0x12A MUI_NO_VALID_SYSTEM_LANGUAGE
- MUI_NO_VALID_SYSTEM_LANGUAGE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MUI_NO_VALID_SYSTEM_LANGUAGE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3d77b9fc4a1e7c739efcd243e7df2df186dc9a25
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839965"
---
# <a name="bug-check-0x12a-mui_no_valid_system_language"></a>Bug 检查0x12A： MUI \_ 没有 \_ 有效的 \_ 系统 \_ 语言


MUI " \_ 没有 \_ 有效 \_ \_ 的系统语言 bug 检查" 的值为 "0x0000012A"。 这表明 Windows 找不到任何已安装的许可语言包（系统默认 UI 语言）。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="mui_no_valid_system_language-parameters"></a>MUI \_ 没有 \_ 有效的 \_ 系统 \_ 语言参数


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
<td align="left">错误检查的子类型
<p>0x1： Windows 在初始化阶段中找不到任何已安装的语言包。</p>
参数 2-描述失败原因的 NT 状态代码。
<p>0x2： Windows 在内核缓存创建过程中找不到任何已安装的许可语言包（系统默认 UI 语言）。</p>
参数 2-描述失败原因的 NT 状态代码。
.</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数1</td>
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

 

 

 




