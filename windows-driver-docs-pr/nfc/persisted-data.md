---
title: 持久保留的数据
description: 数据持久化为。
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b81506d43f4ae901b47e28d6b9b884690309aa1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812755"
---
# <a name="persisted-data"></a>持久保留的数据


注册表位置的数据持久性说明如下所示。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">位置</th>
<th align="left">内容、使用情况、默认值</th>
<th align="left">如果不是默认值，则访问 () </th>
<th align="left">PII 是否已存储？</th>
<th align="left">此设置是否已迁移？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">设备节点注册表位置</td>
<td align="left">NfcRadioTurnedOff，DWORD：
<p>TRUE： NFC RM 已关闭</p>
<p>FALSE： NFC RM 处于开启状态，可使用空闲电源管理</p></td>
<td align="left">继承自设备枚举树，无特殊 ACL 集</td>
<td align="left">空值</td>
<td align="left">否</td>
</tr>
</tbody>
</table>

 

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[ (CX) 参考的 NFC 类扩展](/windows-hardware/drivers/ddi/index)
