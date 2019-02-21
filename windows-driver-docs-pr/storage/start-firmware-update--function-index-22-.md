---
title: 启动固件更新 （函数索引 22）
description: 此函数会初始化到特定固件插槽的固件更新。
ms.assetid: 34950124-6DBF-43CE-862A-E6DEF7A5FADE
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8479001241b1fdfade828f17224174cca17c5ee9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525199"
---
# <a name="start-firmware-update-function-index-22"></a>启动固件更新 （函数索引 22）


此函数会初始化到特定固件插槽的固件更新。 只能有一个在任何给定时间的固件更新操作。

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
<td align="left"><p>正在更新固件插槽。</p></td>
</tr>
</tbody>
</table>

 

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
<p>1：没有当前正在进行的固件更新操作。</p>
<p>转到<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>有关详细信息。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


主机调用以更新和激活固件以下固件函数：

1.  主机调用启动固件更新 (函数索引 22) 以启动固件更新操作。 在此步骤中，该主机选择正在更新的固件插槽。

2.  主机将重复调用[发送固件更新数据 (函数索引 23)](send-firmware-update-data--function-index-23-.md)将数据传输到设备。 每次调用将传输的数据; 区域大小的块主机负责填充如果最后一个传输不是区域大小。

3.  在宿主调用[完成固件更新 (函数索引 24)](finish-firmware-update--function-index-24-.md)将信号发送到固件更新操作已通过的平台。

4.  在宿主调用[选择固件映像槽 (函数索引 25)](select-firmware-image-slot--function-index-25-.md)才能激活新的固件映像。 更新将会在下一步的系统重新启动时生效。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[发送固件更新数据 （函数索引 23）](send-firmware-update-data--function-index-23-.md)

[完成固件更新 （函数索引 24）](finish-firmware-update--function-index-24-.md)

[选择固件映像槽 （函数索引 25）](select-firmware-image-slot--function-index-25-.md)

[获取固件信息 （函数索引 26）](get-firmware-info--function-index-26-.md)

[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






