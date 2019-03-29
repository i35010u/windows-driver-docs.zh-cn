---
Description: WMCDC Device Management Model
title: WMCDC 设备管理模型
ms.localizationpriority: medium
ms.date: 01/07/2019
ms.openlocfilehash: f5a884549c6e16184c8752637743a6ac8e6acddb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575799"
---
# <a name="wmcdc-device-management-model"></a>WMCDC 设备管理模型


USB WMCDC 设备管理模型 (DMM) 接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>通用串行总线 CDC 子类规范适用于无线移动通信设备</em>，1.0，部分 6.6 版。</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>DMM (0X09)。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>任何。</p></td>
</tr>
<tr class="odd">
<td><p>枚举</p></td>
<td><p>是。</p></td>
</tr>
<tr class="even">
<td><p>相关的接口</p></td>
<td><p>无。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_09&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_09
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_09&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_09</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_09&amp;Prot_%02X
USB\Class_02&amp;SubClass_09
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>此控件模型不使用联合功能描述符 (UFD)。</p></td>
</tr>
</tbody>
</table>

 

 

 




