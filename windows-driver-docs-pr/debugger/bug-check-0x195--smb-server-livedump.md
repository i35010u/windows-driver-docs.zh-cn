---
title: Bug 检查 0x195 SMB_SERVER_LIVEDUMP
description: SMB_SERVER_LIVEDUMP bug 检查具有 0x00000195 值。 这表示在 SMB 服务器检测到问题，已捕获核心转储收集调试信息。
ms.assetid: 302BA6E0-DC7C-4AE7-BD4D-C6F6A74D82D9
keywords:
- Bug 检查 0x195 SMB_SERVER_LIVEDUMP
- SMB_SERVER_LIVEDUMP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SMB_SERVER_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 26ba21654e63ae35e551f7b05ff97fec612b2ef5
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350243"
---
# <a name="bug-check-0x195-smbserverlivedump"></a>Bug 检查 0x195：SMB\_SERVER\_LIVEDUMP


SMB\_SERVER\_LIVEDUMP bug 检查的值为 0x00000195。 这表示在 SMB 服务器检测到问题，已捕获核心转储收集调试信息。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="smbserverlivedump-parameters"></a>SMB\_SERVER\_LIVEDUMP 参数


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
<td align="left"><p>0x1:无法在合理的时间内完成 I/O。</p>
2-指针到 I / O 的 SRV2_WORK_ITEM</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数 1</td>
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

 

 

 




