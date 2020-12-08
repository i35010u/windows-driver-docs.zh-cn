---
title: Bug 检查 0x125 NMR_INVALID_STATE
description: NMR_INVALID_STATE bug 检查的值为0x00000125。 这表明)  (网络模块注册器检测到无效状态。 请参阅状态类型的参数1。
keywords:
- Bug 检查 0x125 NMR_INVALID_STATE
- NMR_INVALID_STATE
ms.date: 01/30/2019
topic_type:
- apiref
api_name:
- NMR_INVALID_STATE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c7acca0beb7b2286097cc01cfe456d0bbd05f7bd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816429"
---
# <a name="bug-check-0x125-nmr_invalid_state"></a>Bug 检查0x125： NMR \_ 无效 \_ 状态


NMR \_ 无效 \_ 状态 bug 检查的值为0x00000125。 这表明)  (网络模块注册器检测到无效状态。 请参阅状态类型的参数1。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="nmr_invalid_state-parameters"></a>NMR \_ 无效 \_ 状态参数


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
<td align="left"><p>错误检查的子类型。</p>
<p>0x0：计算机检查异常</p>
<p>参数 2-WHEA_ERROR_RECORD 结构的地址。</p>
<p>参数 3-高阶 32-MCi_STATUS 值的位数。</p>
<p>参数 4-低序位 32-MCi_STATUS 值的位数。</p>
<p>0x1：已更正计算机检查</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。
<p>0x2：已更正平台错误</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。
<p>0x3：不可屏蔽中断</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。
<p>0x4： PCI Express 错误</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。
<p>0x5：一般错误</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。
<p>0x6：初始化错误</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。
<p>0x7：启动错误</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。
<p>0x8：科幻泛型错误</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。
<p>0x9： Itanium 机检查中止</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。
参数 3-SAL 日志的长度（以字节为单位）。
参数 4-SAL 日志的地址。
<p>0xa：已更正 Itanium 计算机检查</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。
<p>0xb：已更正 Itanium 平台错误</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">指向 NMI 句柄的指针</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">指向预期类型的指针（如果可用）</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">预留</td>
</tr>
</tbody>
</table>

 

 

 




