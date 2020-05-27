---
title: 擦除 NVM 图像（功能索引 19）
description: 此函数删除在非易失性内存模块中保存的备份映像。
ms.assetid: D2856D56-413F-4444-9CDF-C42ACA3CFBA0
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c28dffb4c037ab4c24dfef4db7c57cdcf5cfd76c
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851702"
---
# <a name="erase-nvm-image-function-index-19"></a>擦除 NVM 图像（功能索引 19）


此函数删除在非易失性内存模块中保存的备份映像。

> [!NOTE]
> 标有星号（）的所有寄存器 \* 都是在可通过字节寻址的可处理电源接口规范中定义的寄存器。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>送


### <a name="span-idargs3spanspan-idargs3spanspan-idargs3spanargs3"></a><span id="Args3"></span><span id="args3"></span><span id="ARGS3"></span>Args3

无。

## <a name="span-idoutputspanspan-idoutputspanspan-idoutputspanoutput"></a><span id="Output"></span><span id="output"></span><span id="OUTPUT"></span>输出


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段</th>
<th align="left">字节长度</th>
<th align="left">字节偏移量</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>状态</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>此函数可以返回以下特定于函数的错误代码：</p>
<p>1：操作超时。</p>
<p>有关详细信息，请参阅<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>。</p></td>
</tr>
</tbody>
</table>

 

> [!NOTE]
> 这是一个同步函数。 仅当擦除操作已完成或超时时，它才返回。如果操作所用的时间超过在 \* *erase \_ TIMEOUT0* （0，0x1E）和 \* *erase \_ TIMEOUT1* （0，0x1F）中定义的超时时间，则平台应在返回前中止此函数。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[\_用于字节寻址的支持能源的函数类的 DSM 接口（Function Interface 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






