---
title: 完成固件更新（功能索引 24）
description: 此函数完成固件更新操作，该操作将启动对启动固件更新（函数索引22）的调用。
ms.assetid: 1A9446D7-67F7-4AC2-8784-BFC05A0EA608
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a03704278c2b3b57ddce081acf25a7f4dcf8932b
ms.sourcegitcommit: dff3834724bd5204c4a47204540fe8125dd37b20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2019
ms.locfileid: "70750056"
---
# <a name="finish-firmware-update-function-index-24"></a>完成固件更新（功能索引 24）


此函数完成固件更新操作，该操作将[启动对启动固件更新（函数索引22）](start-firmware-update--function-index-22-.md)的调用。

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
<th align="left">定义域</th>
<th align="left">字节长度</th>
<th align="left">字节偏移</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>状态值</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>此函数可以返回以下特定于函数的错误代码：</p>
<p>1:没有正在进行的固件更新操作。</p>
<p>2:固件映像无效。</p>
<p>有关详细信息，请参阅<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[启动固件更新（函数索引22）](start-firmware-update--function-index-22-.md)

[发送固件更新数据（函数索引23）](send-firmware-update-data--function-index-23-.md)

[选择固件图像槽（函数索引25）](select-firmware-image-slot--function-index-25-.md)

[获取固件信息（函数索引26）](get-firmware-info--function-index-26-.md)

[\_用于字节寻址的支持能源的函数类的 DSM 接口（Function Interface 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






