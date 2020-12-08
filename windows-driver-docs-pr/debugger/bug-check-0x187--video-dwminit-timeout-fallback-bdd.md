---
title: Bug 检查 0x187 VIDEO_DWMINIT_TIMEOUT_FALLBACK_BDD
description: VIDEO_DWMINIT_TIMEOUT_FALLBACK_BDD bug 检查的值为0x00000187。 这表明视频退回 BDD，而不是使用 IHV 驱动程序。 这始终会生成实时转储。
keywords:
- Bug 检查 0x187 VIDEO_DWMINIT_TIMEOUT_FALLBACK_BDD
- VIDEO_DWMINIT_TIMEOUT_FALLBACK_BDD
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_DWMINIT_TIMEOUT_FALLBACK_BDD
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3a8905177e44918ef2fe4d696a2c523d84c9c6fa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814013"
---
# <a name="bug-check-0x187-video_dwminit_timeout_fallback_bdd"></a>Bug 检查0x187：视频 \_ DWMINIT \_ 超时 \_ 回退 \_ BDD


视频 \_ DWMINIT \_ TIMEOUT \_ 回退 \_ BDD bug 检查的值为0x00000187。 这表明视频退回 BDD，而不是使用 IHV 驱动程序。 这始终会生成实时转储。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="video_dwminit_timeout_fallback_bdd-parameters"></a>视频 \_ DWMINIT \_ 超时 \_ 回退 \_ BDD 参数


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
<td align="left">原因代码。
<p>0x1：在重试后 DWM 无法初始化，停止显示适配器并回退到 BDD</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">预留</td>
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

 

 

 




