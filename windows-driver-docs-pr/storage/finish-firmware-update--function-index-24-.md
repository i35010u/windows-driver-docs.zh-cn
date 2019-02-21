---
title: 完成固件更新 （函数索引 24）
description: 此函数完成对启动固件更新 (函数索引 22) 的调用启动的固件更新操作。
ms.assetid: 1A9446D7-67F7-4AC2-8784-BFC05A0EA608
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a03704278c2b3b57ddce081acf25a7f4dcf8932b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533505"
---
# <a name="finish-firmware-update-function-index-24"></a>完成固件更新 （函数索引 24）


此函数完成固件更新操作的调用[启动固件更新 (函数索引 22)](start-firmware-update--function-index-22-.md)启动。

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>输入


### <a name="span-idargs3spanspan-idargs3spanspan-idargs3spanargs3"></a><span id="Args3"></span><span id="args3"></span><span id="ARGS3"></span>Args3

无。

## <a name="span-idoutputspanspan-idoutputspanspan-idoutputspanoutput"></a><span id="Output"></span><span id="output"></span><span id="OUTPUT"></span>Output


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
<th align="left">字节偏移</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>状态</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>此函数可返回以下特定于函数的错误代码：</p>
<p>1：没有固件更新操作正在进行中。</p>
<p>2：无效的固件映像。</p>
<p>转到<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>有关详细信息。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[启动固件更新 （函数索引 22）](start-firmware-update--function-index-22-.md)

[发送固件更新数据 （函数索引 23）](send-firmware-update-data--function-index-23-.md)

[选择固件映像槽 （函数索引 25）](select-firmware-image-slot--function-index-25-.md)

[获取固件信息 （函数索引 26）](get-firmware-info--function-index-26-.md)

[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






