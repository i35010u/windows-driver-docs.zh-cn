---
Description: CDC 多渠道 ISDN 控制模型
title: CDC 多渠道 ISDN 控制模型
ms.localizationpriority: medium
ms.date: 01/07/2019
ms.openlocfilehash: 90c99ca91bbf616aa7150790ccd9edd15386ce6e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392101"
---
# <a name="cdc-multi-channel-isdn-control-model"></a>CDC 多渠道 ISDN 控制模型


USB CDC 多渠道 ISDN 控制模型 (MCCM) 接口集合具有以下属性。

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
<td><p><em>通用串行总线类定义通信设备</em>，版本 1.1 中，部分 3.7.1</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02)</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>MCCM (0x04)</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00)</p></td>
</tr>
<tr class="odd">
<td><p>枚举</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>相关的接口</p></td>
<td><p>联合功能描述符 (UFD) 引用的多个数据类接口。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_04&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_04
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_04&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_04</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_04&amp;Prot_00
USB\Class_02&amp;SubClass_04
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>

 

 

 




