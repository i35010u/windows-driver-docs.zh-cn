---
title: Bug 检查 0x193 VIDEO_DXGKRNL_LIVEDUMP
description: VIDEO_DXGKRNL_LIVEDUMP bug 检查的值为0x00000193。 这表明发生了由 dxgkrnl 触发的 livedump。
ms.assetid: 73B84617-7DBB-4161-BAB3-8BCDDBE9BE93
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
ms.openlocfilehash: 04e61840d2e2f69b1de86996152cb92b11a1ffb6
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534834"
---
# <a name="bug-check-0x193-video_dxgkrnl_livedump"></a>Bug 检查0x193： VIDEO \_ DXGKRNL \_ LIVEDUMP


视频 \_ DXGKRNL \_ LIVEDUMP bug 检查的值为0x00000193。 这表明发生了由 dxgkrnl 触发的 livedump。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="video_dxgkrnl_livedump-parameters"></a>视频 \_ DXGKRNL \_ LIVEDUMP 参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">说明</th>
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
<td align="left">保留</td>
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

## <a name="resolution"></a>解决方法
[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
 

 

 




