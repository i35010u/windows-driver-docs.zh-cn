---
title: 使用四个未压缩的图面进行解码
description: 使用四个未压缩的图面进行解码
keywords:
- 视频解码 WDK DirectX VA，顺序要求
- 解码视频 WDK DirectX VA，顺序要求
- 图片解码 WDK DirectX VA，顺序要求
- 序列要求 WDK DirectX VA
- 连续要求 WDK DirectX VA
- 用于解码 WDK DirectX VA 的多个未压缩的图面
- 用于解码 WDK DirectX VA 的未压缩曲面示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6c7dd8347230c099c546b17c9c6edc27977f433
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818545"
---
# <a name="using-four-uncompressed-surfaces-for-decoding"></a>使用四个未压缩的图面进行解码


## <span id="ddk_using_four_uncompressed_surfaces_for_decoding_gg"></span><span id="DDK_USING_FOUR_UNCOMPRESSED_SURFACES_FOR_DECODING_GG"></span>


下表显示了一个假设情况，其中视频解码器需要一段时间才能对每张照片进行解码。 此方法对位流进行解码，其中包含了在第一张图片之后从零个图片开始，从零个图片开始的 B 图片。 B 张图片的位流会在一对 P 图片之间出现。 在此表中，字母显示每张图片的类型 (I，B 或 P) ，下标显示框架显示索引 (每个图片) 的临时显示顺序，而上标显示包含该图片的缓冲区的数目。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">已解码图片</th>
<th align="left">显示的图片</th>
<th align="left">时间间隔开始时 (解码帧) </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>我⁰₀</p></td>
<td align="left"></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>P ¹₁</p></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>P ²₃</p></td>
<td align="left"><p>我⁰₀</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="even">
<td align="left"><p>B ³₂</p></td>
<td align="left"><p>P ¹₁</p></td>
<td align="left"><p>3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>P ⁰₆</p></td>
<td align="left"><p>B ³₂</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="even">
<td align="left"><p>B ¹₄</p></td>
<td align="left"><p>P ²₃</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B ³₅</p></td>
<td align="left"><p>B ¹₄</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="even">
<td align="left"><p>P ²₁₀</p></td>
<td align="left"><p>B ³₅</p></td>
<td align="left"><p>7</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B ¹₇</p></td>
<td align="left"><p>P ⁰₆</p></td>
<td align="left"><p>8</p></td>
</tr>
<tr class="even">
<td align="left"><p>B ³₈</p></td>
<td align="left"><p>B ¹₇</p></td>
<td align="left"><p>9</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B ¹₉</p></td>
<td align="left"><p>B ³₈</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="even">
<td align="left"><p>P ⁰₁₅</p></td>
<td align="left"><p>B ¹₉</p></td>
<td align="left"><p>11</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B ³₁₁</p></td>
<td align="left"><p>P ²₁₀</p></td>
<td align="left"><p>12</p></td>
</tr>
<tr class="even">
<td align="left"><p>B ¹₁₂</p></td>
<td align="left"><p>B ³₁₁</p></td>
<td align="left"><p>13</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B ³₁₃</p></td>
<td align="left"><p>B ¹₁₂</p></td>
<td align="left"><p>14</p></td>
</tr>
<tr class="even">
<td align="left"><p>B ¹₁₄</p></td>
<td align="left"><p>B ³₁₃</p></td>
<td align="left"><p>15</p></td>
</tr>
<tr class="odd">
<td align="left"><p>P ²₂₁</p></td>
<td align="left"><p>B ¹₁₄</p></td>
<td align="left"><p>16</p></td>
</tr>
<tr class="even">
<td align="left"><p>B ³₁₆</p></td>
<td align="left"><p>P ²₂₁</p></td>
<td align="left"><p>17</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B ¹₁₇</p></td>
<td align="left"><p>B ³₁₆</p></td>
<td align="left"><p>18</p></td>
</tr>
<tr class="even">
<td align="left"><p>B ³₁₈</p></td>
<td align="left"><p>B ¹₁₇</p></td>
<td align="left"><p>19</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B ¹₁₉</p></td>
<td align="left"><p>B ³₁₈</p></td>
<td align="left"><p>20</p></td>
</tr>
<tr class="even">
<td align="left"><p>B ³₂₀</p></td>
<td align="left"><p>B ¹₁₉</p></td>
<td align="left"><p>21</p></td>
</tr>
<tr class="odd">
<td align="left"><p>P ⁰₂₈</p></td>
<td align="left"><p>B ³₂₀</p></td>
<td align="left"><p>22</p></td>
</tr>
</tbody>
</table>

 

上表中的每个 B 图片需要按位流顺序对前两个图片进行解码，然后才能对其进行解码。 因此，在解码第三个) 时间段之前，解码器无法使用正确的计时开始显示图片，直到第二个图片被解码 (。 在此时间段内的某个位置，可以开始显示正确计时的图片。

显示图片时，显示的图片可能并不完全一致。 相反，显示可能会继续在发送以显示的图片之前显示一个图片，直到正确的时间到达即可切换到新图片。 为了获得最佳性能，第0面 (，其中包含第一个 "我的图片") 不应覆盖在以后到达三帧时间的 B 图片使用，即使 B 图片不需要使用 "我的图片" 进行引用。 而是应使用第三个图面 (第3面) 来保存该 B 图片。 这样就无需检查第一张图片的显示期间是否已完成，然后解码 B 图片。

解码器 [顺序要求](sequence-requirements.md) 中所述的两个规则要求每个前三个已解码图片置于不同的图面中，因为在第三个阶段 (第2期) 之前，它们都未显示。 然后，第四个解码图片应置于第四个图面中，这是因为在第四个阶段中，在第四个阶段 (第3次) 时，显示的第一个图片可能尚未结束。

解码过程中的一个重要障碍是，在两个以上的 B 图片连续出现的结果。 在上表中，出现第十个解码图片 (B ¹₉) 。 当遇到连续系列中的第三个或后续 B 图片时，将消除显示一张 B 图片和使用曲面来保存下一个解码 B 图片之间的时间延迟。 主机解码器必须检查上一期中显示的 B 图片的显示状态 (B ¹₇) ，以确保已从显示中删除该图片 (等待此操作在必要的情况下进行) ，则它必须立即使用同一图面对下一个 B 图片进行解码 (图面 1) 用于 B ¹₉。 解码器无法将新的 B 图片解码到用于保存其引用 I 或 P 图片 (的图面中，这种情况下，用于 P ⁰₆和 P ²₁₀) 的图面0和2，并且无法将新的 B 图片解码为在同一时间间隔内显示的表面 (，这种情况下，适用于 B ³₈) 。 因此，它必须使用前一段中显示的表面 (在本例中为 surface 1) 。

 

 





