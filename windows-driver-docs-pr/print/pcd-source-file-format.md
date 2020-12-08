---
title: PCD 源文件格式
description: PCD 源文件格式
keywords:
- 绘图仪驱动程序 WDK 打印，微型驱动程序
- MSPlot WDK 打印，微型驱动程序
- 微型驱动程序 WDK MSPlot
- PCD 文件 WDK MSPlot
- pcd 文件
- 关键字 WDK MSPlot
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed8852d426c8fa254c9369db3d75ba5869d7c512
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807625"
---
# <a name="pcd-source-file-format"></a>PCD 源文件格式





使用以下格式指定所有绘图仪设备特征：

*关键字* { *value* }

其中， *关键字* 是 PCD 源文件关键字之一， *值* 为带引号的字符串或数字值。 例如，下面的语句指定绘图仪支持颜色：

```cpp
ColorCap {1}
```

下表描述了关键字。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>关键字</th>
<th>值定义</th>
<th>默认值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>BezierCap</strong></p></td>
<td><p>1 = 设备支持 HPGL2 贝塞尔扩展。</p>
<p>0 = 不支持。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>ColorCap</strong></p></td>
<td><p>1 = 颜色设备</p>
<p>0 = 单色设备</p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>COLORINFO</strong></p></td>
<td><p>三十个 DWORD 大小的值，表示 <a href="/windows/win32/api/winddi/ns-winddi-colorinfo" data-raw-source="[&lt;strong&gt;COLORINFO&lt;/strong&gt;](/windows/win32/api/winddi/ns-winddi-colorinfo)"><strong>COLORINFO</strong></a> 结构的内容。</p></td>
<td><p></p>
{ {6810,3050,0} ，//xr，年，年 {2260,6550,0} ，//xg，Yg，yg {1810,500,0} ，//xb，yb，yb {2000,2450,0} ，//Xc，yc，yc {5210,2100,0} ，//，ym，ym {4750,5100,0} ，//xy，yy，yy {3324,3474,10000} ，//xw，yw，yw 10000，10000，10000，//RGB 伽玛1422952，//m/c，y/C 787495，//c/y，m/y} 324248</td>
</tr>
<tr class="even">
<td><p><strong>DeviceMargin</strong></p></td>
<td><p>四个 DWORD 大小的值，表示左、上、右和下纸张的边距，以 1/1000 mm 单位表示。</p></td>
<td><p></p>
{5000，5000，5000，36000}</td>
</tr>
<tr class="odd">
<td><p><strong>DeviceName</strong></p></td>
<td><p>带引号的字符串，表示最大 (31 个字符的可显示设备名称 ) </p></td>
<td><p>"HPGL/2 个绘图仪"</p></td>
</tr>
<tr class="even">
<td><p><strong>DevicePelsDPI</strong></p></td>
<td><p>一个 DWORD 大小的值，表示设备的有效 DPI。 有关详细信息，请参阅<a href="/windows/win32/api/winddi/ns-winddi-gdiinfo" data-raw-source="[&lt;strong&gt;GDIINFO&lt;/strong&gt;](/windows/win32/api/winddi/ns-winddi-gdiinfo)"><strong>GDIINFO</strong></a>的<strong>upDevicePelsDPI</strong>成员。</p></td>
<td><p>默认值为零，导致 GDI 计算值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceSize</strong></p></td>
<td><p>两个 DWORD 大小的值，表示最大纸张大小（以 1/1000 mm 单位的 <em>x</em> 和 <em>y</em> 坐标表示）。</p>
<p><em>Y</em>值 25400 (1 英寸) 或更少表示设备接受可变纸张长度。</p></td>
<td><p></p>
{215900，279400}</td>
</tr>
<tr class="even">
<td><p><strong>FormInfo</strong></p></td>
<td><p>绘图仪支持的每个窗体的窗体说明。 有关详细信息，请参阅此表后面的 <strong>窗体说明</strong> 部分。</p></td>
<td><p>无。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HTPatternSize</strong></p></td>
<td><p>标识标准半色调模式的 HT_PATSIZE_ 前缀的常量之一。</p></td>
<td><p>0xffffffff</p></td>
</tr>
<tr class="even">
<td><p><strong>InitString</strong></p></td>
<td><p>带引号的 C 语言字符串，表示驱动程序的 <a href="/windows/win32/api/winddi/nf-winddi-drvstartpage" data-raw-source="[&lt;strong&gt;DrvStartPage&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvstartpage)"><strong>DrvStartPage</strong></a> 函数发送到打印机的命令。</p></td>
<td><p>空字符串。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxCopies</strong></p></td>
<td><p>设备可呈现的每页最大副本数。</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxPens</strong></p></td>
<td><p> (32 的笔数 ) </p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxPolygonPts</strong></p></td>
<td><p>定义要绘制或填充多边形的最大点数。</p></td>
<td><p>128</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxQuality</strong></p></td>
<td><p>质量级别 (4 最大值 ) </p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxScale</strong></p></td>
<td><p>最大缩放大小。 0-10000 (100 为 100% ) </p></td>
<td><p>100</p></td>
</tr>
<tr class="even">
<td><p><strong>NoBitmapFont</strong></p></td>
<td><p>1 = 设备不支持位图字体。</p>
<p>0 = 支持位图字体。</p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>PaperTrayCap</strong></p></td>
<td><p>1 = 设备有纸器源。</p>
<p>0 = 不支持。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>PaperTraySize</strong></p></td>
<td><p>两个 DWORD 大小的值，表示纸盒的宽度和高度（以 1/1000 mm 单位表示）。</p></td>
<td><p></p>
{-1，-1}</td>
</tr>
<tr class="odd">
<td><p><strong>PlotDPI</strong></p></td>
<td><p>两个 DWORD 大小的值，表示画笔的 <em>x</em> 和 <em>y</em> 分辨率（以每英寸点数为单位）。</p></td>
<td><p></p>
{1016，1016}</td>
</tr>
<tr class="even">
<td><p><strong>PlotPenData</strong></p></td>
<td><p>每笔的笔说明。 有关详细信息，请参阅此表后面的 " <strong>笔说明</strong> " 部分。</p></td>
<td><p>无。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PushPopPal</strong></p></td>
<td><p>1 = 在 RTL 和 HPGL2 之间切换时，驱动程序必须推送/弹出面板。</p>
<p>0 = 不需要推送/弹出。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>RasterByteAlign</strong></p></td>
<td><p>1 = 设备必须接收以字节对齐的 x 坐标表示的所有光栅数据。</p>
<p>0 = 不需要字节对齐。</p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>RasterCap</strong></p></td>
<td><p>1 = 光栅设备</p>
<p>0 = 笔设备</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>RasterDPI</strong></p></td>
<td><p>两个 DWORD 大小的值，表示 <em>x</em> 和 <em>y</em> 分辨率（以每英寸点数为单位）。</p>
<p>对于光栅绘图仪，这是光栅分辨率。</p>
<p>对于笔式绘图仪，这是对应用程序的 GDI 提供的理想解决方案。</p></td>
<td><p></p>
{300，300}</td>
</tr>
<tr class="odd">
<td><p><strong>RollFeedCap</strong></p></td>
<td><p>1 = 设备有卷纸来源。</p>
<p>0 = 不支持。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>ROPLevel</strong></p></td>
<td><p>ROP_LEVEL_0 = 不支持 RasterOp。</p>
<p>ROP_LEVEL_1 = Rop1 支持。</p>
<p>ROP_LEVEL_2 = Rop2 支持。</p>
<p>ROP_LEVEL_3 = Rop3 支持。</p></td>
<td><p>ROP_LEVEL_0</p></td>
</tr>
<tr class="odd">
<td><p><strong>RTLMonoEncode5</strong></p></td>
<td><p>1 = 支持 RTL 光栅传输语言 (RTL) 单色压缩模式5。</p>
<p>0 = 不支持。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>RTLMonoFixPal</strong></p></td>
<td><p>仅 RTL 单色调色板。</p>
<p>0 = 白色，1 = 黑色</p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>RTLMonoNoCID</strong></p></td>
<td><p>1 = 在 RTL Mono 模式下，不需要 CID 命令。</p>
<p>0 = 在 RTL Mono 模式下，需要 CID 命令。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>RTLNoDPIxy</strong></p></td>
<td><p>1 = RTL DPI X，不支持 Y 移动命令。</p>
<p>0 = 支持这些命令。</p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>TransparentCap</strong></p></td>
<td><p>1 = 设备支持透明模式。</p>
<p>0 = 不支持。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>WindingFillCap</strong></p></td>
<td><p>1 = 设备支持缠绕填充。</p>
<p>0 = 不支持。</p></td>
<td><p>0</p></td>
</tr>
</tbody>
</table>

 

### <a name="pen-descriptions"></a><a href="" id="ddk-pen-descriptions-gg"></a>笔说明

每个笔说明必须具有以下格式：

**PlotPenData {**<em>笔号</em>**，** <em>Color</em>**}**

其中， *笔号* 标识笔的槽编号， *颜色* 为 PC \_ IDX-带 \_ 前缀的颜色标识符。 下面是笔说明的示例：

```cpp
PlotPenData {1, PC_IDX_WHITE}
PlotPenData {2, PC_IDX_BLACK}
PlotPenData {3, PC_IDX_RED}
```

### <a name="form-descriptions"></a><a href="" id="ddk-form-descriptions-gg"></a>窗体说明

每个窗体说明必须具有以下格式：

**FormInfo {"**<em>窗体说明</em>**"，** <em>宽度</em>**，** <em>长度</em>**，** <em>左边距</em>**，** <em>上边距</em>**，** <em>右页边距</em>**，** <em>下边距</em>**}**

其中， *窗体说明* 是一个描述窗体的字符串， *宽度* 和 *长度* 指定窗体大小（以 1/1000 mm 单位为单位），并且还在 1/1000 mm 单位中指定边距。 下面是三个示例：

```cpp
FormInfo {"Roll Paper 24 in",    609600,      0, 0, 0, 0, 0}
FormInfo {"ANSI A 8.5 x 11 in",  215900, 279400, 0, 0, 0, 0}
FormInfo {"ISO A4 210 x 297 mm", 210000, 297000, 0, 0, 0, 0}
```

