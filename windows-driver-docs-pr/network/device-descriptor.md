---
title: 设备描述符
description: 设备描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b66695ecaeb0fca83397db2caaf9481e159ee74a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817589"
---
# <a name="device-descriptor"></a>设备描述符





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
<td align="left"><p>0x12</p></td>
<td align="left"><p>此描述符的大小（以字节为单位）</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>bDescriptorType</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x01</p></td>
<td align="left"><p>设备描述符</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>bcdUSB</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>0x0110</p></td>
<td align="left"><p>1.1-当前版本的 USB 规范</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>bDeviceClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x02</p></td>
<td align="left"><p>通信设备类</p></td>
</tr>
<tr class="odd">
<td align="left"><p>5</p></td>
<td align="left"><p>bDeviceSubClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>未使用</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>bDeviceProtocol</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>未使用</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7</p></td>
<td align="left"><p>bMaxPacketSize0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x08</p></td>
<td align="left"><p>控制管道上的最大数据包大小</p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>idVendor</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>0xXXXX</p></td>
<td align="left"><p>供应商 ID</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>idProduct</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>0xXXXX</p></td>
<td align="left"><p>产品 ID</p></td>
</tr>
<tr class="even">
<td align="left"><p>12</p></td>
<td align="left"><p>bcdDevice</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>0xXXXX</p></td>
<td align="left"><p>设备发行代码</p></td>
</tr>
<tr class="odd">
<td align="left"><p>14</p></td>
<td align="left"><p>iManufacturer</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x01</p></td>
<td align="left"><p>制造商字符串的索引</p></td>
</tr>
<tr class="even">
<td align="left"><p>15</p></td>
<td align="left"><p>iProduct</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x02</p></td>
<td align="left"><p>产品字符串索引</p></td>
</tr>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>iSerialNumber</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x03</p></td>
<td align="left"><p>设备序列号字符串的索引</p></td>
</tr>
<tr class="even">
<td align="left"><p>17</p></td>
<td align="left"><p>bNumConfigurations</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x01</p></td>
<td align="left"><p>一个配置</p></td>
</tr>
</tbody>
</table>

 

 

 





