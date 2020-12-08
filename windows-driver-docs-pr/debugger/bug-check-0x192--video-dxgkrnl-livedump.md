---
title: Bug 检查 0x193 VIDEO_DXGKRNL_LIVEDUMP
description: VIDEO_DXGKRNL_LIVEDUMP bug 检查的值为0x00000193。 这表明发生了由 dxgkrnl 触发的 livedump。
keywords:
- Bug 检查 0x193 VIDEO_DXGKRNL_LIVEDUMP
- VIDEO_DXGKRNL_LIVEDUMP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_DXGKRNL_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f0621d948b6d582f85ba5df56314f98d7466e214
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837353"
---
# <a name="bug-check-0x193-video_dxgkrnl_livedump"></a>Bug 检查0x193： VIDEO \_ DXGKRNL \_ LIVEDUMP


视频 \_ DXGKRNL \_ LIVEDUMP bug 检查的值为0x00000193。 这表明发生了由 dxgkrnl 触发的 livedump。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="video_dxgkrnl_livedump-parameters"></a>视频 \_ DXGKRNL \_ LIVEDUMP 参数


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
<td align="left"><p>原因代码</p>
0x100 内部</td>
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

## <a name="resolution"></a>解决方法
[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
 

 

 




