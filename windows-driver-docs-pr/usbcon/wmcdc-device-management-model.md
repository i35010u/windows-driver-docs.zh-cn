---
Description: WMCDC 设备管理模型
title: WMCDC 设备管理模型
ms.localizationpriority: medium
ms.date: 01/07/2019
ms.openlocfilehash: 81849e1e2b1fa86332d264b106b6798b090050ab
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161583"
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
<td><p>Protocol</p></td>
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
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_09&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_09
USB\Vid_%04x&Pid_%04x&Cdc_09&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_09</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_09&Prot_%02X
USB\Class_02&SubClass_09
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>此控件模型不使用联合功能描述符 (UFD)。</p></td>
</tr>
</tbody>
</table>

 

 

 




