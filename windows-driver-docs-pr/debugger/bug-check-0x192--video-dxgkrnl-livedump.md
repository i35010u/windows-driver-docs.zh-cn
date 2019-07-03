---
title: Bug 检查 0x193 VIDEO_DXGKRNL_LIVEDUMP
description: VIDEO_DXGKRNL_LIVEDUMP bug 检查具有 0x00000193 值。 这表明由 dxgkrnl 触发 livedump 发生。
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
ms.openlocfilehash: 267afdca7b9e47ae1d8ac06172df7614ef3e9693
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519819"
---
# <a name="bug-check-0x193-videodxgkrnllivedump"></a>Bug 检查 0x193：VIDEO\_DXGKRNL\_LIVEDUMP


视频\_DXGKRNL\_LIVEDUMP bug 检查的值为 0x00000193。 这表明由 dxgkrnl 触发 livedump 发生。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="videodxgkrnllivedump-parameters"></a>视频\_DXGKRNL\_LIVEDUMP 参数


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

## <a name="resolution"></a>分辨率
[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息，有助于在确定根本原因。
 

 

 




