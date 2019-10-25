---
title: 持久保留的数据
description: 数据持久化为。
ms.assetid: 61C3C55C-00DC-4A8C-B235-7C0391FB5119
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9475f20a802adec7143a609ce510e86ae7cec4d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834056"
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
<th align="left">Access （如果不是默认值）</th>
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
<td align="left">N/A</td>
<td align="left">无</td>
</tr>
</tbody>
</table>

 

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC 类扩展（CX）参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

