---
title: 麦克风阵列几何描述符格式
description: 麦克风阵列几何描述符格式
ms.assetid: 83fae1e2-cc67-4322-8250-f642508383ef
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44385111ec6915d66e18a78358fe1ae365e12e6e
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925546"
---
# <a name="microphone-array-geometry-descriptor-format"></a>麦克风阵列几何描述符格式

USB 音频麦克风阵列必须向它所连接到的系统说明自身。 这意味着必须将描述数组所需的参数嵌入到数组设备本身中。 使用**GET\_MEM**请求从设备检索阵列几何信息。

有关 USB 音频设备几何图形的信息必须以标准格式提供。 同样，旨在使用 Windows Vista USB 音频类驱动程序的 USB 麦克风阵列必须提供使用下表中定义的信息格式的描述符。

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
<th align="left">偏移量</th>
<th align="left">字段</th>
<th align="left">大小</th>
<th align="left">值</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>guidMicArrayID</p></td>
<td align="left"><p>16</p></td>
<td align="left"><p>全局唯一标识符 (GUID) </p></td>
<td align="left"><p>一个唯一的 ID，用于在内存（{07FE86C1-8948-4db5-B184-C5162D4AD314}）中标记麦克风阵列信息的开头。</p></td>
</tr>
<tr class="even">
<td align="left"><p>16</p></td>
<td align="left"><p>wDescriptorLength</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>麦克风阵列信息的长度（以字节为单位），包括 GUID 和长度字段。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>18</p></td>
<td align="left"><p>wVersion</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>二进制编码的十进制（BCD）</p></td>
<td align="left"><p>麦克风阵列规范的版本号，后跟此描述符。</p></td>
</tr>
<tr class="even">
<td align="left"><p>20</p></td>
<td align="left"><p>wMicArrayType</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>定义以下值：</p>
<p>00：线性。</p>
<p>01：平面。</p>
<p>02: 3-三维（3D）。</p>
<p>03-FFFF：已保留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>22</p></td>
<td align="left"><p>wWorkVertAngBeg</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>工作音量垂直角度的起点。</p></td>
</tr>
<tr class="even">
<td align="left"><p>24</p></td>
<td align="left"><p>wWorkVertAngEnd</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>工作音量垂直角度的结束。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>26</p></td>
<td align="left"><p>wWorkHorAngBeg</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>工作音量水平角的开头。</p></td>
</tr>
<tr class="even">
<td align="left"><p>28</p></td>
<td align="left"><p>wWorkHorAngEnd</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>工作音量水平角度的结束。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>30</p></td>
<td align="left"><p>wWorkFreqBandLo</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>工作频率范围的下限。</p></td>
</tr>
<tr class="even">
<td align="left"><p>32</p></td>
<td align="left"><p>wWorkFreqBandHi</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>工作频率范围的上限。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>34</p></td>
<td align="left"><p>wNumberOfMics</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>后面的各个麦克风定义的数量。</p></td>
</tr>
<tr class="even">
<td align="left"><p>36</p></td>
<td align="left"><p>wMicrophoneType （0）</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>用于唯一标识麦克风0类型的数字：</p>
<p>00：全方位</p>
<p>01： SubCardioid</p>
<p>02： Cardioid</p>
<p>03： SuperCardioid</p>
<p>04： HyperCardioid</p>
<p>05: 8 形</p>
<p>0F-FF：定义的供应商</p></td>
</tr>
<tr class="odd">
<td align="left"><p>38</p></td>
<td align="left"><p>wXCoordinate （0）</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>麦克风0的 x 坐标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>40</p></td>
<td align="left"><p>wYCoordinate （0）</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>麦克风0的 y 坐标。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>42</p></td>
<td align="left"><p>wZCoordinate （0）</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>麦克风0的 z 坐标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>44</p></td>
<td align="left"><p>wMicVertAngle （0）</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>麦克风0的主响应轴（MRA）垂直角度。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>46</p></td>
<td align="left"><p>wMicHorAngle （0）</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>麦克风0的 MRA 水平角。</p></td>
</tr>
<tr class="even">
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
<td align="left"><p>麦克风定义1到 n-2。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>34 + （（n-1）<em>12)</p></td>
<td align="left"><p>wMicType （n-1）</p></td>
<td align="left"></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>用于唯一标识麦克风 n-1 类型的数字：</p>
<p>00：全方位</p>
<p>01： SubCardioid</p>
<p>02： Cardioid</p>
<p>03： SuperCardioid</p>
<p>04： HyperCardioid</p>
<p>05: 8 形</p>
<p>0F-FF：定义的供应商</p></td>
</tr>
<tr class="even">
<td align="left"><p>36 + （（n-1）</em>12）</p></td>
<td align="left"><p>wXCoordinate （n-1）</p></td>
<td align="left"></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>麦克风 n-1 的 x 坐标。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>38 + （（n-1）<em>12)</p></td>
<td align="left"><p>wYCoordinate （n-1）</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>麦克风 n-1 的 y 坐标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>40 + （（n-1）</em>12）</p></td>
<td align="left"><p>wZCoordinate （n-1）</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>麦克风 n-1 的 z 坐标。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>42 + （（n-1）<em>12)</p></td>
<td align="left"><p>wMicVertAngle （n-1）</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>麦克风 MRA 的垂直角度为-1。</p></td>
</tr>
<tr class="even">
<td align="left"><p>44 + （（n-1）</em>12）</p></td>
<td align="left"><p>wMicHorAngle （n-1）</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>麦克风 MRA 的水平角。</p></td>
</tr>
</tbody>
</table>

有关如何在4元素麦克风阵列的描述符中使用此信息格式的详细示例，请参阅附录 A[如何构建和使用适用于 Windows Vista 的麦克风阵列](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/MicArrays_guide.doc)白皮书。

**注意**  

-   在麦克风数组信息中包含版本号时，它允许在实现原始规范后更新描述符。 版本号为 BCD 值。 例如，当前版本（1.0）表示为0x0100。

-   偏移量和大小值以字节为单位。

-   所有角度以1/10000 弧度为单位表示。 例如，3.1416 弧度表示为31416。 此值的范围为-31416 到31416（含）。

-   X y z 坐标以毫米表示。 此值的范围为-32767 到32767（含）。

-   有关坐标系统角度、轴和正面方向的信息，请参阅上面提到的麦克风阵列白皮书中的附录 B。

-   频率值用 Hz 表示。 Frequency 值的范围仅受**wWorkFreqBandLo**到**wWorkFreqBandHi**字段的大小限制。
