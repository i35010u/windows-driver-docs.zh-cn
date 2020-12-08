---
title: 配置描述符
description: 配置描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ee8525afc8abdb17c236a03df77519a5b913034
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840657"
---
# <a name="configuration-descriptor"></a>配置描述符





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
<th align="left">Offset</th>
<th align="left">字段</th>
<th align="left">大小</th>
<th align="left">值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>bLength</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x09</p></td>
<td align="left"><p>此描述符的大小（以字节为单位）</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>bDescriptorType</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x02</p></td>
<td align="left"><p>配置描述符</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>wTotalLength</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>0x003E</p></td>
<td align="left"><p>总配置块的长度，包括此描述符和所有以下说明符（以字节为单位）</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>bNumInterfaces</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x02</p></td>
<td align="left"><p>两个接口</p></td>
</tr>
<tr class="odd">
<td align="left"><p>5</p></td>
<td align="left"><p>bConfigurationValue</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x01</p></td>
<td align="left"><p>此配置的 ID</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>iConfiguration</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>未使用</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7</p></td>
<td align="left"><p>bmAttributes</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x80</p></td>
<td align="left"><p>总线电源</p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>MaxPower</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x64</p></td>
<td align="left"><p>200 mA</p></td>
</tr>
</tbody>
</table>

 

 

 





