---
title: CC 类别
description: CC 类别
keywords:
- 流类别 WDK 视频捕获，隐藏式分类
- CC 类别 WDK 视频捕获
- PINNAME_VIDEO_CC
- 隐藏式类别的 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bc27074032e48ad1bac8cc105ba5a530a46234c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839359"
---
# <a name="cc-category"></a>CC 类别


以下 GUID 对应于隐藏式 (CC) 类别：

-   **PINNAME \_ 视频 \_ 抄送**

    CC 类别输出插针提供来自第1行、第21行的解码的已解码的字节对流。

指定 **PINNAME \_ 视频 \_ CC** pin 时，使用下表中列出的信息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DataRange 结构</strong></p></td>
<td><p>KS_DATARANGE</p></td>
</tr>
<tr class="even">
<td><p><strong>DataFormat 结构</strong></p></td>
<td><p>KS_DATAFORMAT</p></td>
</tr>
<tr class="odd">
<td><p><strong>主要格式 GUID</strong></p></td>
<td><p>KSDATAFORMAT_TYPE_AUXLine21Data</p></td>
</tr>
<tr class="even">
<td><p><strong>子格式 GUID</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_Line21_BytePair</p></td>
</tr>
<tr class="odd">
<td><p><strong>说明符 GUID</strong></p></td>
<td><p>KSDATAFORMAT_SPECIFIER_NONE</p></td>
</tr>
<tr class="even">
<td><p><strong>扩展的标头大小</strong></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>必需的属性集</strong></p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p><strong>必需的事件集</strong></p></td>
<td><p>无</p></td>
</tr>
<tr class="odd">
<td><p><strong>DirectShow majortype</strong></p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p><strong>DirectShow formattype</strong></p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>

 

 

 




