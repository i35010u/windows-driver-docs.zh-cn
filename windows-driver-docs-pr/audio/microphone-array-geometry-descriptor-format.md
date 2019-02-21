---
title: 麦克风阵列 Geometry 描述符格式
description: 麦克风阵列 Geometry 描述符格式
ms.assetid: 83fae1e2-cc67-4322-8250-f642508383ef
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99d8b688d21a898ca0b726d5bc3bd0a2a57b2de3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541680"
---
# <a name="microphone-array-geometry-descriptor-format"></a>麦克风阵列 Geometry 描述符格式


USB 音频麦克风阵列必须描述自身到连接到系统。 这意味着需要描述数组的参数必须嵌入数组设备本身。 阵列几何信息通过从设备中检索**获取\_内存优化**请求。

必须采用标准格式提供有关 USB 音频设备几何信息。 在这种情况下，旨在能够与 Windows Vista USB 音频类驱动程序的 USB 麦克风阵列必须提供使用下表中定义的信息格式的描述符。

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
<th align="left">尺寸</th>
<th align="left">值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>guidMicArrayID</p></td>
<td align="left"><p>16</p></td>
<td align="left"><p>全局唯一标识符 (GUID)</p></td>
<td align="left"><p>表示的内存 ({07FE86C1-8948-4db5-B184-C5162D4AD314}) 中的麦克风阵列信息开头的唯一 ID。</p></td>
</tr>
<tr class="even">
<td align="left"><p>16</p></td>
<td align="left"><p>wDescriptorLength</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>麦克风阵列信息，包括 GUID 和长度的字段长度以字节为单位。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>18</p></td>
<td align="left"><p>wVersion</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>二进制编码的十进制 (BCD)</p></td>
<td align="left"><p>麦克风阵列规范，此说明符后跟的版本号。</p></td>
</tr>
<tr class="even">
<td align="left"><p>20</p></td>
<td align="left"><p>wMicArrayType</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>定义以下值：</p>
<p>00:线性。</p>
<p>01:平面数据。</p>
<p>02:三维 (3D)。</p>
<p>03 FFFF:保留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>22</p></td>
<td align="left"><p>wWorkVertAngBeg</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>工作卷垂直角度的开始日期。</p></td>
</tr>
<tr class="even">
<td align="left"><p>24</p></td>
<td align="left"><p>wWorkVertAngEnd</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>工作卷垂直角度的末尾。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>26</p></td>
<td align="left"><p>wWorkHorAngBeg</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>工作卷水平角度的起始处。</p></td>
</tr>
<tr class="even">
<td align="left"><p>28</p></td>
<td align="left"><p>wWorkHorAngEnd</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>工作卷水平角度的末尾。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>30</p></td>
<td align="left"><p>wWorkFreqBandLo</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>工作频率范围下限。</p></td>
</tr>
<tr class="even">
<td align="left"><p>32</p></td>
<td align="left"><p>wWorkFreqBandHi</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>工作频率范围的上限。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>34</p></td>
<td align="left"><p>wNumberOfMics</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>遵循的各个麦克风定义的数量。</p></td>
</tr>
<tr class="even">
<td align="left"><p>36</p></td>
<td align="left"><p>wMicrophoneType(0)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>一个唯一标识的麦克风 0 类型的数字：</p>
<p>00:全方位</p>
<p>01:SubCardioid</p>
<p>02:Cardioid</p>
<p>03:SuperCardioid</p>
<p>04:HyperCardioid</p>
<p>05:8 形状</p>
<p>0F-FF:供应商定义</p></td>
</tr>
<tr class="odd">
<td align="left"><p>38</p></td>
<td align="left"><p>wXCoordinate(0)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>麦克风 0 x 坐标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>40</p></td>
<td align="left"><p>wYCoordinate(0)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>麦克风 0 y 坐标。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>42</p></td>
<td align="left"><p>wZCoordinate(0)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>麦克风 0 z 轴坐标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>44</p></td>
<td align="left"><p>wMicVertAngle(0)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>主要响应 （设备） 轴垂直的麦克风 0 的角度。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>46</p></td>
<td align="left"><p>wMicHorAngle(0)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>麦克风 0 设备水平角度。</p></td>
</tr>
<tr class="even">
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
<td align="left"><p>麦克风定义 1 到 n-2。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>34+((n-1)<em>12)</p></td>
<td align="left"><p>wMicType(n-1)</p></td>
<td align="left"></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>唯一标识的麦克风 n-1 类型数：</p>
<p>00:全方位</p>
<p>01:SubCardioid</p>
<p>02:Cardioid</p>
<p>03:SuperCardioid</p>
<p>04:HyperCardioid</p>
<p>05:8 形状</p>
<p>0F-FF:供应商定义</p></td>
</tr>
<tr class="even">
<td align="left"><p>36+((n-1)</em>12)</p></td>
<td align="left"><p>wXCoordinate(n-1)</p></td>
<td align="left"></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>麦克风 n-1 x 坐标。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>38+((n-1)<em>12)</p></td>
<td align="left"><p>wYCoordinate(n-1)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>麦克风 n-1 y 坐标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>40+((n-1)</em>12)</p></td>
<td align="left"><p>wZCoordinate(n-1)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>麦克风 n-1 z 轴坐标。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>42+((n-1)<em>12)</p></td>
<td align="left"><p>wMicVertAngle(n-1)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>设备垂直的麦克风 n-1 角度。</p></td>
</tr>
<tr class="even">
<td align="left"><p>44+((n-1)</em>12)</p></td>
<td align="left"><p>wMicHorAngle(n-1)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>编号</p></td>
<td align="left"><p>麦克风 n-1 设备水平角度。</p></td>
</tr>
</tbody>
</table>

 

有关如何使用此信息格式的描述符中的 4 元素麦克风阵列的详细示例，请参阅的附录 A[如何与生成和使用麦克风阵列适用于 Windows Vista 的](https://go.microsoft.com/fwlink/p/?linkid=306613)白皮书。

**注意**  

 

-   麦克风阵列信息中包含的版本号，这样的描述符进行更新后的原始的规范实现。 版本编号是 BCD 值。 例如，当前版本 (1.0) 表示为 0x0100。

-   偏移量和大小的值是以字节为单位。

-   所有的角度表示的 1/10000 弧度为单位。 例如，3.1416 弧度为单位表示为 31416。 该值的范围可以从-31416 到 31416，非独占。

-   X y z 坐标来表示以毫米为单位。 该值的范围是-32767 到 32767 之间 （含）。

-   有关方向、 轴和坐标系统的角度正方向的信息，请参阅麦克风阵列白皮书中的附录 B。

-   以赫兹表示频率值。 频率值的范围仅受中的字段的大小**wWorkFreqBandLo**到**wWorkFreqBandHi**。

 

 




