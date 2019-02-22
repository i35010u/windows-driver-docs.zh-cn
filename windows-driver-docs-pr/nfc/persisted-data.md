---
title: 保留的数据
description: 是数据暂留。
ms.assetid: 61C3C55C-00DC-4A8C-B235-7C0391FB5119
keywords:
- NFC
- 附近通信
- 近程
- 邻近附近
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b01ed73a76b4f3caa0001a791f48d54049df05c2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545229"
---
# <a name="persisted-data"></a>保留的数据


下面介绍了注册表位置的数据持久性。

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
<th align="left">内容，使用情况，默认值</th>
<th align="left">访问权限 （如果不是默认值）</th>
<th align="left">PII 存储？</th>
<th align="left">此设置迁移？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">设备节点注册表位置</td>
<td align="left">NfcRadioTurnedOff，DWORD:
<p>TRUE:NFC RM 处于关闭状态</p>
<p>FALSE:NFC RM 会上并受到空闲电源管理</p></td>
<td align="left">从设备枚举树中，没有特殊的 ACL 设置继承</td>
<td align="left">不适用</td>
<td align="left">否</td>
</tr>
</tbody>
</table>

 

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC 类扩展 (CX) 引用](https://msdn.microsoft.com/library/windows/hardware/dn905536)  

