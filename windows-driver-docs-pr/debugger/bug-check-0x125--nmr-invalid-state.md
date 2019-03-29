---
title: Bug 检查 0x125 NMR_INVALID_STATE
description: NMR_INVALID_STATE bug 检查具有 0x00000125 值。 这表示 NMR （网络模块注册机构） 已检测到无效的状态。 请参阅状态类型的参数 1。
ms.assetid: DD80FC61-8211-46A0-9D44-CF1E729B12D4
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
ms.openlocfilehash: e1bc1b6a9b6a16402cb616fe0b0fbe1e6b5f48e8
ms.sourcegitcommit: 598259684cbfcf39b16dcc91bd8d341b43fb8876
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/13/2019
ms.locfileid: "56582799"
---
# <a name="bug-check-0x125-nmrinvalidstate"></a>Bug 检查 0x125：NMR\_无效\_状态


NMR\_无效\_状态 bug 检查的值为 0x00000125。 这表示 NMR （网络模块注册机构） 已检测到无效的状态。 请参阅状态类型的参数 1。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="nmrinvalidstate-parameters"></a>NMR\_无效\_状态参数


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
<td align="left"><p>检测的错误子类型。</p>
<p>0x0:计算机检查异常</p>
<p>参数 2-WHEA_ERROR_RECORD 结构的地址。</p>
<p>参数 3-MCi_STATUS 值的高顺序 32-位。</p>
<p>参数 4-MCi_STATUS 值的低顺序 32 位。</p>
<p>0x1:更正计算机检查</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。
<p>0x2:已更正的平台错误</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。
<p>0x3:不可屏蔽的中断</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。
<p>0x4:PCI Express Error</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。
<p>0x5:常规错误</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。
<p>0x6:初始化错误</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。
<p>0x7:启动错误</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。
<p>0x8:名工商管理学博士一般性错误</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。
<p>0x9:Itanium 计算机检查中止</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。
参数 3 的 SAL 日志的长度 （字节）。
参数 4-SAL 日志的地址。
<p>0xa:Itanium 更正计算机检查</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。
<p>0xb:Itanium 更正平台错误</p>
参数 2-WHEA_ERROR_RECORD 结构的地址。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">指向 NMI 句柄</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">指向时可用的预期类型</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">保留</td>
</tr>
</tbody>
</table>

 

 

 




