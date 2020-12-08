---
title: Bug 检查 0x195 SMB_SERVER_LIVEDUMP
description: SMB_SERVER_LIVEDUMP bug 检查的值为0x00000195。 这表明 SMB 服务器检测到问题并已捕获内核转储来收集调试信息。
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
ms.openlocfilehash: 383bcbf3e6a3eb4b21478a476f9da3da8e7a466d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820961"
---
# <a name="bug-check-0x195-smb_server_livedump"></a>Bug 检查0x195： SMB \_ 服务器 \_ LIVEDUMP


SMB \_ 服务器 \_ LIVEDUMP bug 检查的值为0x00000195。 这表明 SMB 服务器检测到问题并已捕获内核转储来收集调试信息。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="smb_server_livedump-parameters"></a>SMB \_ 服务器 \_ LIVEDUMP 参数


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
<td align="left"><p>0x1： i/o 未能在合理的时间内完成。</p>
2-指向 i/o 的 SRV2_WORK_ITEM 的指针</td>
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

 

 

 




