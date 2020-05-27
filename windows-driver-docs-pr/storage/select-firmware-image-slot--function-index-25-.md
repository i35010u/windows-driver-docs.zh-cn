---
title: 选择固件映像槽（功能索引 25）
description: 此函数选择哪个固件映像处于活动状态。
ms.assetid: 65B8BF11-4377-455A-9A08-0C15FADC0BBC
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 03858a7aaa6c4a2525175b91c94452c42100ad8d
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851256"
---
# <a name="select-firmware-image-slot-function-index-25"></a>选择固件映像槽（功能索引 25）


此函数选择哪个固件映像处于活动状态。 在设备重置时，应加载所选图像。

> [!NOTE]
> 标有星号（）的所有寄存器 \* 都是在可通过字节寻址的可处理电源接口规范中定义的寄存器。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>送


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
<th align="left">字节偏移量</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>固件槽</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>在设备重置时，应选择为 "活动" 的固件映像槽。</p></td>
</tr>
</tbody>
</table>

 

> [!NOTE]
> 固件应将**固件槽**值写入 \* *FW \_ 槽 \_ 信息*（3，0x42）寄存器的下4位。

 

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
<p>1：槽编号无效。</p>
<p>2：此槽中没有映像。</p>
<p>有关详细信息，请参阅<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[启动固件更新（功能索引 22）](start-firmware-update--function-index-22-.md)

[发送固件更新数据（功能索引 23）](send-firmware-update-data--function-index-23-.md)

[完成固件更新（功能索引 24）](finish-firmware-update--function-index-24-.md)

[获取固件信息（功能索引 26）](get-firmware-info--function-index-26-.md)

[\_用于字节寻址的支持能源的函数类的 DSM 接口（Function Interface 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






