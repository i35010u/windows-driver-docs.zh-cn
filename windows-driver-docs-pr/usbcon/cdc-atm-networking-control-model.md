---
Description: CDC ATM 网络控制模型
title: CDC ATM 网络控制模型
ms.localizationpriority: medium
ms.date: 01/07/2019
ms.openlocfilehash: 944b79021e43676cbdfa7992cb15876442f14cc5
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161365"
---
# <a name="cdc-atm-networking-control-model"></a>CDC ATM 网络控制模型


USB CDC ATM 网络控制模型 (ANCM) 接口集合具有以下属性。

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
<td><p><em>通用串行总线类定义通信设备</em>，版本 1.1 中，部分 3.8.3 将现有</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02)</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>ANCM (0x07)</p></td>
</tr>
<tr class="even">
<td><p>Protocol</p></td>
<td><p>无 (0x00)</p></td>
</tr>
<tr class="odd">
<td><p>枚举</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>相关的接口</p></td>
<td><p>通过联合功能描述符 (UFD) 引用的一个数据类接口</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_07&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_07
USB\Vid_%04x&Pid_%04x&Cdc_07&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_07</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_07&Prot_00
USB\Class_02&SubClass_07
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>

 

 

 




