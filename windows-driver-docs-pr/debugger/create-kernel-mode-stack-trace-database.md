---
title: 创建内核模式堆栈跟踪数据库
description: 创建内核模式堆栈跟踪数据库
ms.assetid: 0c1f94c0-ebc7-4e3c-8101-ba3cf830e7f8
keywords:
- 创建内核模式堆栈跟踪数据库 （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0b92527797d311c111c96a104c3e89100c02892
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523222"
---
# <a name="create-kernel-mode-stack-trace-database"></a>创建内核模式堆栈跟踪数据库


## <span id="ddk_create_kernel_mode_stack_trace_database_dtools"></span><span id="DDK_CREATE_KERNEL_MODE_STACK_TRACE_DATABASE_DTOOLS"></span>


**创建内核模式堆栈跟踪数据库**标志创建运行时堆栈跟踪数据库的内核操作，例如资源对象和对象管理操作，并仅适用于使用的 Windows 内部的版本。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>kst</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x2000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_KERNEL_STACK_TRACE_DB</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>整个系统的注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

GFlags 将此标志显示为一个内核标志，该标志设置，但它是无效的运行时，因为内核已经启动。

 

 





