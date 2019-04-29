---
title: 使用四个未压缩的图面进行解码
description: 使用四个未压缩的图面进行解码
ms.assetid: ceeea614-6793-4a75-8334-7dd062ac0b46
keywords:
- 视频解码 WDK DirectX va，因此序列要求
- 解码视频 WDK DirectX va，因此序列要求
- 解码 WDK DirectX va，因此序列要求的图片
- 序列化要求 WDK DirectX VA
- 连续要求 WDK DirectX VA
- 用于解码 WDK DirectX VA 的多个未压缩的图面
- 用于解码 WDK DirectX VA 的未压缩的图面示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c02155fd59e9ef392f04a00564abd84bb8400708
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389034"
---
# <a name="using-four-uncompressed-surfaces-for-decoding"></a>使用四个未压缩的图面进行解码


## <span id="ddk_using_four_uncompressed_surfaces_for_decoding_gg"></span><span id="DDK_USING_FOUR_UNCOMPRESSED_SURFACES_FOR_DECODING_GG"></span>


下表显示了视频解码器需要一个帧时间进行解码的每张图片的假设情况。 它将解码包含稳步越来越多的从零个 B 图片开始后我想象着一个初始的 B 图片位流。 对之间的 P 图片出现 B 图片的位流。 在此表中，以字母显示每张图片 （我、 B 或 P） 的类型、 下标显示帧显示索引 （临时显示每张图片的顺序），和上标显示包含图片的缓冲区数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">解码后的图片</th>
<th align="left">显示的图片</th>
<th align="left">帧 Decoded （在间隔的开头）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>I⁰₀</p></td>
<td align="left"></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>P¹₁</p></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>P²₃</p></td>
<td align="left"><p>I⁰₀</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="even">
<td align="left"><p>B³₂</p></td>
<td align="left"><p>P¹₁</p></td>
<td align="left"><p>3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>P⁰₆</p></td>
<td align="left"><p>B³₂</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="even">
<td align="left"><p>B¹₄</p></td>
<td align="left"><p>P²₃</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B³₅</p></td>
<td align="left"><p>B¹₄</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="even">
<td align="left"><p>P²₁₀</p></td>
<td align="left"><p>B³₅</p></td>
<td align="left"><p>7</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B¹₇</p></td>
<td align="left"><p>P⁰₆</p></td>
<td align="left"><p>8</p></td>
</tr>
<tr class="even">
<td align="left"><p>B³₈</p></td>
<td align="left"><p>B¹₇</p></td>
<td align="left"><p>9</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B¹₉</p></td>
<td align="left"><p>B³₈</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="even">
<td align="left"><p>P⁰₁₅</p></td>
<td align="left"><p>B¹₉</p></td>
<td align="left"><p>11</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B³₁₁</p></td>
<td align="left"><p>P²₁₀</p></td>
<td align="left"><p>12</p></td>
</tr>
<tr class="even">
<td align="left"><p>B¹₁₂</p></td>
<td align="left"><p>B³₁₁</p></td>
<td align="left"><p>13</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B³₁₃</p></td>
<td align="left"><p>B¹₁₂</p></td>
<td align="left"><p>14</p></td>
</tr>
<tr class="even">
<td align="left"><p>B¹₁₄</p></td>
<td align="left"><p>B³₁₃</p></td>
<td align="left"><p>15</p></td>
</tr>
<tr class="odd">
<td align="left"><p>P²₂₁</p></td>
<td align="left"><p>B¹₁₄</p></td>
<td align="left"><p>16</p></td>
</tr>
<tr class="even">
<td align="left"><p>B³₁₆</p></td>
<td align="left"><p>P²₂₁</p></td>
<td align="left"><p>17</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B¹₁₇</p></td>
<td align="left"><p>B³₁₆</p></td>
<td align="left"><p>18</p></td>
</tr>
<tr class="even">
<td align="left"><p>B³₁₈</p></td>
<td align="left"><p>B¹₁₇</p></td>
<td align="left"><p>19</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B¹₁₉</p></td>
<td align="left"><p>B³₁₈</p></td>
<td align="left"><p>20</p></td>
</tr>
<tr class="even">
<td align="left"><p>B³₂₀</p></td>
<td align="left"><p>B¹₁₉</p></td>
<td align="left"><p>21</p></td>
</tr>
<tr class="odd">
<td align="left"><p>P⁰₂₈</p></td>
<td align="left"><p>B³₂₀</p></td>
<td align="left"><p>22</p></td>
</tr>
</tbody>
</table>

 

上表中每个 B 图片需要解码位流顺序中的两个先前图片之前可以解码。 因此，解码器不能开始后 （即，直到在过程中的解码的第三个时间段） 解码后第二个图显示具有之前其正确的时间安排的图片。 某个位置在此时间段，具有其正确的时间安排的图片显示可以开始。

图片显示用于启动不可能用在显示屏显示的图片完全一致。 而是显示可能会继续显示之前显示适当的时候到达，若要切换到新图片之前发送的那个图片。 为用于引用该 B 图片不需要使用到达三个帧时间更高版本，即使我想象着让 B 图片，不应以获得最佳性能，覆盖面 0 （其中包含我的图片的第一个）。 相反，应使用第四个面 （面 3） 来保存该 B 图片。 这消除了需要检查是否已解码 B 图片之前完成的第一个我的图片的显示时间。

两个规则中所述[序列化要求](sequence-requirements.md)解码器需要将每个已解码的前三个图片置于中不同的图面，因为其中任何一个具有第三个时间段 （在某个时间，才显示句点 2）。 然后，第四个解码的图片应将放在第四个面，因为第一个显示的图片的显示可能不会转移到第四个时间段 （段 3） 内的某些时。

在解码过程中的明显障碍出现由于连续会发生两个以上 B 图片。 在上表中遇到的第十个解码的图片 (B¹₉) 后发生这种情况。 当遇到连续系列中的第三个或后续 B 图片时，消除了一个 B 图片的显示图面来保存下一个已解码的 B 图片使用之间的滞后时间公差。 主机解码器必须检查下一步 B pictur 在以前的时间段 (B¹₇) 以确保已从显示 （等待这种情况发生，如有必要），则它必须立即使用相同的图面中显示的 B 图片的显示状态e，为已解码 （面用于 B¹₉ 1）。 解码器无法解码的面被用来保存它的引用，我或 P 图片 （在本例中，图面 0 和 2 用于 P⁰₆ 和 P²₁₀），并不能解码为 t 的相同时间间隔内显示的图面新 B 图片的任意一个新的 B 图片（在此情况下，图 3 用于 B³₈ 面） 的输入法。 因此，它必须使用在前面紧邻的时间段 （以这种情况下，图面上 1) 中显示的图面。

 

 





