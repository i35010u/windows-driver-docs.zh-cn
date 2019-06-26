---
title: PCD 源文件格式
description: PCD 源文件格式
ms.assetid: 8651d6ca-7cd7-4c07-aa66-2766dd2222e0
keywords:
- 绘图器驱动程序 WDK 打印，微型驱动程序
- MSPlot WDK 打印，微型驱动程序
- 微型驱动程序 WDK MSPlot
- PCD 文件 WDK MSPlot
- .pcd 文件
- 关键字 WDK MSPlot
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a030e9d66d6bdbead4d6ed7e15cf34a12b3ca434
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360697"
---
# <a name="pcd-source-file-format"></a>PCD 源文件格式





使用以下格式指定所有绘图器设备特征：

*keyword* { *value* }

其中*关键字*PCD 源之一是文件关键字和*值*是带引号的字符串或数字值。 例如，以下语句指定绘图器支持颜色：

```cpp
ColorCap {1}
```

下表所述的关键字。

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
<td><p>1 = 设备支持 HPGL2 贝赛尔曲线扩展。</p>
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
<td><p>三十大小 DWORD 的值表示的内容<a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_colorinfo" data-raw-source="[&lt;strong&gt;COLORINFO&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_colorinfo)"> <strong>COLORINFO</strong> </a>结构。</p></td>
<td><p></p>
{ {6810,3050,0}，/ / xr，年，年{2260,6550,0}，/ / xg，yg，Yg {1810,500,0}，/ / xb，yb，Yb {2000,2450,0}，/ / xc，yc，Yc {5210,2100,0}，/ / xm，ym，Ym {4750,5100,0}，/ / xy，yy、 Yy {3324,3474,10000}，/ / xw，yw，Yw 10000,10000,10000，/ / RGB gamma 1422,952，/ / M/C，Y/C 787,495，/ / C/M Y/M 324,248 / / C/Y Y M /}</td>
</tr>
<tr class="even">
<td><p><strong>DeviceMargin</strong></p></td>
<td><p>四个大小 DWORD 的值表示左侧、 顶部、 右侧和底部纸张边距，以 1/1000 个毫米为单位。</p></td>
<td><p></p>
{5000, 5000, 5000, 36000}</td>
</tr>
<tr class="odd">
<td><p><strong>DeviceName</strong></p></td>
<td><p>带引号的字符串表示可显示设备名称 （31 个字符最大）。</p></td>
<td><p>"HPGL/2 绘图仪"</p></td>
</tr>
<tr class="even">
<td><p><strong>DevicePelsDPI</strong></p></td>
<td><p>一个大小 DWORD 的值，表示设备的有效 DPI。 有关详细信息请参阅<strong>upDevicePelsDPI</strong>的成员<a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_gdiinfo" data-raw-source="[&lt;strong&gt;GDIINFO&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_gdiinfo)"> <strong>GDIINFO</strong></a>。</p></td>
<td><p>默认值为零，从而导致 GDI 来计算的值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceSize</strong></p></td>
<td><p>表示最大纸张的两个大小 DWORD 的值调整大小，请在<em>x</em>并<em>y</em>坐标的 1/1000 个 mm 单位。</p>
<p>一个<em>y</em>小于或等于 25400 （1 英寸） 的值指示设备接受变量纸张长度。</p></td>
<td><p></p>
{215900, 279400}</td>
</tr>
<tr class="even">
<td><p><strong>FormInfo</strong></p></td>
<td><p>关于支持的绘图器每个窗体的窗体说明。 有关详细信息，请参阅<strong>窗体说明</strong>此表后面的部分。</p></td>
<td><p>无。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HTPatternSize</strong></p></td>
<td><p>确定标准半色调模式 HT_PATSIZE_ 前缀常量之一。</p></td>
<td><p>0xffffffff</p></td>
</tr>
<tr class="even">
<td><p><strong>InitString</strong></p></td>
<td><p>带引号的 C 语言字符串，表示发送到打印机的驱动程序的命令<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartpage" data-raw-source="[&lt;strong&gt;DrvStartPage&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartpage)"> <strong>DrvStartPage</strong> </a>函数。</p></td>
<td><p>NULL 字符串。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxCopies</strong></p></td>
<td><p>每个设备可以呈现的页的副本的最大数目。</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxPens</strong></p></td>
<td><p>数量的笔 (最大值 32)。</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxPolygonPts</strong></p></td>
<td><p>用于定义要对其应用笔划或填充的多边形的点的最大数目。</p></td>
<td><p>128</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxQuality</strong></p></td>
<td><p>数量的质量级别 (最大 4)。</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxScale</strong></p></td>
<td><p>最大的规模大小。 0 到 10000 （100 是 100%）</p></td>
<td><p>100</p></td>
</tr>
<tr class="even">
<td><p><strong>NoBitmapFont</strong></p></td>
<td><p>1 = 设备不支持 bitmap 字体。</p>
<p>0 = 支持字体的位图。</p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>PaperTrayCap</strong></p></td>
<td><p>1 = 设备具有纸张来源送纸器。</p>
<p>0 = 不支持。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>PaperTraySize</strong></p></td>
<td><p>两个大小 DWORD 的值表示纸张送纸器宽度和高度，以 1/1000 个毫米为单位。</p></td>
<td><p></p>
{-1, -1}</td>
</tr>
<tr class="odd">
<td><p><strong>PlotDPI</strong></p></td>
<td><p>两个大小 DWORD 的值表示笔绘图仪<em>x</em>并<em>y</em>分辨率，以每英寸点数。</p></td>
<td><p></p>
{1016, 1016}</td>
</tr>
<tr class="even">
<td><p><strong>PlotPenData</strong></p></td>
<td><p>关于每个笔的笔说明。 有关详细信息，请参阅<strong>笔说明</strong>此表后面的部分。</p></td>
<td><p>无。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PushPopPal</strong></p></td>
<td><p>1 = 驱动程序必须推送/弹出面板 RTL 和 HPGL2 之间切换时。</p>
<p>0 = 推送/弹出不是必需的。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>RasterByteAlign</strong></p></td>
<td><p>1 = 设备必须在收到所有光栅数据字节对齐 x 坐标。</p>
<p>0 = 字节对齐方式不是必需的。</p></td>
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
<td><p>两个大小 DWORD 的值表示<em>x</em>并<em>y</em>分辨率，以每英寸点数。</p>
<p>对于光栅绘图仪，这是光栅解析。</p>
<p>对于笔式绘图仪，这是理想的解决办法 GDI 提供给应用程序。</p></td>
<td><p></p>
{300, 300}</td>
</tr>
<tr class="odd">
<td><p><strong>RollFeedCap</strong></p></td>
<td><p>1 = 设备已回滚纸张来源。</p>
<p>0 = 不支持。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>ROPLevel</strong></p></td>
<td><p>ROP_LEVEL_0 = 否 RasterOp 支持。</p>
<p>ROP_LEVEL_1 = Rop1 支持。</p>
<p>ROP_LEVEL_2 = Rop2 支持。</p>
<p>ROP_LEVEL_3 = Rop3 支持。</p></td>
<td><p>ROP_LEVEL_0</p></td>
</tr>
<tr class="odd">
<td><p><strong>RTLMonoEncode5</strong></p></td>
<td><p>1 = HP 光栅传输语言 (RTL) 支持单色压缩模式 5。</p>
<p>0 = 不支持。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>RTLMonoFixPal</strong></p></td>
<td><p>RTL 单色调色板。</p>
<p>0 = 白色，1 = 黑色</p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>RTLMonoNoCID</strong></p></td>
<td><p>1 = 在 RTL Mono 模式中，CID 命令不是必需的。</p>
<p>0 = 在 RTL Mono 模式中，CID 命令都是必需。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>RTLNoDPIxy</strong></p></td>
<td><p>1 = RTL DPI X，Y 移动不支持命令。</p>
<p>0 = 这些支持命令。</p></td>
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
<td><p>1 = 出现在缠绕填充设备支持。</p>
<p>0 = 不支持。</p></td>
<td><p>0</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-pen-descriptions-gg"></a>笔说明

每个笔说明必须具有以下格式：

**PlotPenData {** <em>笔数</em> **，** <em>颜色</em> **}**

其中*笔数*标识钢笔的插槽编号和*颜色*是 PC\_IDX\_-前缀颜色标识符。 以下是示例笔说明：

```cpp
PlotPenData {1, PC_IDX_WHITE}
PlotPenData {2, PC_IDX_BLACK}
PlotPenData {3, PC_IDX_RED}
```

### <a href="" id="ddk-form-descriptions-gg"></a>窗体说明

每个窗体的说明必须具有以下格式：

**FormInfo {"** <em>形成说明</em> **"，** <em>宽度</em> **，** <em>长度</em> **，** <em>左边距</em> **，** <em>上边距</em> **，** <em>右键边距</em> **，** <em>底部边距</em> **}**

其中*窗体说明*是一个字符串，描述窗体，*宽度*并*长度*1/1000 个毫米为单位，指定窗体大小和 1/1000 个 mm 中还指定了边距单位。 以下是三个示例：

```cpp
FormInfo {"Roll Paper 24 in",    609600,      0, 0, 0, 0, 0}
FormInfo {"ANSI A 8.5 x 11 in",  215900, 279400, 0, 0, 0, 0}
FormInfo {"ISO A4 210 x 297 mm", 210000, 297000, 0, 0, 0, 0}
```

 

 




