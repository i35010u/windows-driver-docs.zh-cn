---
title: 选择固件映像槽 （函数索引 25）
description: 此函数选择的固件映像处于活动状态。
ms.assetid: 65B8BF11-4377-455A-9A08-0C15FADC0BBC
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: db61d647aabb4c20f6006d3bc348773eb80f9f08
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524270"
---
# <a name="select-firmware-image-slot-function-index-25"></a>选择固件映像槽 （函数索引 25）


此函数选择的固件映像处于活动状态。 当设备重置时，应加载所选的映像。

&gt; \[!请注意\]    &gt;用一个星号标记所有寄存器 (\*) 字节可寻址能源支持接口规范中定义的寄存器。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>输入


### <a name="span-idargs3spanspan-idargs3spanspan-idargs3spanargs3"></a><span id="Args3"></span><span id="args3"></span><span id="ARGS3"></span>Args3

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
<td align="left"><strong>个固件插槽</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>应选择为活动时设备将重置固件映像槽。</p></td>
</tr>
</tbody>
</table>

 

&gt; \[!请注意\]    &gt;固件应编写**个固件插槽**值到较低的 4 位\**转发\_槽\_信息*（3，0x42） 注册。

 

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
<p>1：无效的槽数。</p>
<p>2：此槽中没有的图像。</p>
<p>转到<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>有关详细信息。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[启动固件更新 （函数索引 22）](start-firmware-update--function-index-22-.md)

[发送固件更新数据 （函数索引 23）](send-firmware-update-data--function-index-23-.md)

[完成固件更新 （函数索引 24）](finish-firmware-update--function-index-24-.md)

[获取固件信息 （函数索引 26）](get-firmware-info--function-index-26-.md)

[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






