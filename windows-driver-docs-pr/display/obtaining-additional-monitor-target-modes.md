---
title: 获取其他监视目标模式
description: 获取其他监视目标模式
ms.assetid: fc0e2d43-8fc2-4757-ba77-f72a01e04343
keywords:
- 监视器目标模式 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9481aa19a9e238df3021b6587369df9de8b2678
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840525"
---
# <a name="obtaining-additional-monitor-target-modes"></a>获取其他监视目标模式


从 Windows 7 开始，提供了一个新的监视界面， [**DXGK\_监视\_接口\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_monitor_interface_v2)。 它提供了两个不在原始[**DXGK\_监视器\_interface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_monitor_interface)接口中的其他函数：

[**pfnGetAdditionalMonitorModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_getadditionalmonitormodeset)

[**pfnReleaseAdditionalMonitorModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_releaseadditionalmonitormodeset)

这些函数为显示微型端口驱动程序提供了一种动态且可缩放的方式，用于向 VidPN 目标添加目标模式。 相比之下，DXGK\_MONITOR\_INTERFACE 接口仅提供目标模式的静态列表。 使用这些函数，驱动程序可以在操作系统中查询它应枚举的其他模式的列表。 驱动程序可以验证请求的模式并拒绝监视器不支持的模式。

当显示微型端口驱动程序收到对驱动程序实现的[**DxgkDdiEnumVidPnCofuncModality**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)函数的调用以枚举目标模式时，

它应使用以下过程向目标模式集添加兼容的计时信息：

1.  返回在调用[**pfnGetAdditionalMonitorModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_getadditionalmonitormodeset)时所获取的已筛选的附加目标模式。 它还应返回常规目标模式，如[枚举 Cofunctional VidPN 源和目标模式](enumerating-cofunctional-vidpn-source-and-target-modes.md)中所述。

2.  **PfnGetAdditionalMonitorModeSet**函数将返回以下内容：
    -   *ppAdditionalModesSet*， [**DXGK\_TARGETMODE\_详细\_计时**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgk_targetmode_detail_timing)格式的其他计时模式的列表。
    -   *pNumberModes，* 计时模式的数目。

3.  循环访问所有这些计时模式。

4.  筛选出所有不兼容的计时模式，以及在调用*DxgkDdiEnumVidPnCofuncModality*期间已经提供的所有常规模式。

5.  将剩余计时模式转换为[**D3DKMDT\_VIDPN\_目标\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_target_mode)类型。

6.  将所有剩余计时模式添加到 VidPN 目标模式集。

7.  调用[**pfnReleaseAdditionalMonitorModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_releaseadditionalmonitormodeset) ，以释放从**pfnGetAdditionalMonitorModeSet**返回的其他计时模式列表。

显示微型端口驱动程序应将硬件支持的所有其他计时模式添加到 VidPN 源模式集和目标模式集。 当显示模式管理器（CALL CENTER.DMM）生成模式列表时，监视器不支持的所有显示模式（包括附加计时模式）都将被指定为不受监视器支持，并且仅显示在 "原始模式" 列表中。 无论监视器是否已连接，微型端口驱动程序都应报告监视器支持的所有 VidPN 源和目标模式集。 仅报告监视支持模式的驱动程序还必须报告当前连接的监视器不支持的其他模式。

## <a name="crt-monitors"></a>CRT 监视器

对于 CRT 监视器，CALL CENTER.DMM 作为附加的目标模式添加了 640 x 480 x 60Hz 标准监视器计时，该时间是在视频电子标准协会（VESA）规范中定义的， *VESA 和行业标准以及计算机显示器的准则计时版本 1.0*。

## <a name="dtv-and-hdtv-monitors"></a>DTV 和 HDTV 监视器

对于数字电视（DTV）和高清晰电视（HDTV）监视器，CALL CENTER.DMM 添加为其他目标模式[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)自动测试图形-0043 所需的所有标准 DTV 模式，如下表所示。 显示微型端口驱动程序应会修剪显示硬件不支持的所有模式。

**59.95 hz DTV 系统：**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DTV 格式</th>
<th align="left">HDTV 格式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>640 x 480p x 59.94 Hz，高宽比比4:3</p></td>
<td align="left"><p>640 x 480p x 59.94 Hz，高宽比比4:3</p></td>
</tr>
<tr class="even">
<td align="left"><p>720（1440） x 480i x 59.94 Hz，宽高比4:3</p></td>
<td align="left"><p>720（1440） x 480i x 59.94 Hz，宽高比4:3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>720（1440） x 480i x 59.94 Hz，宽高比16:9</p></td>
<td align="left"><p>720（1440） x 480i x 59.94 Hz，宽高比16:9</p></td>
</tr>
<tr class="even">
<td align="left"><p>720 x 480p x 59.94 Hz，高宽比比4:3</p></td>
<td align="left"><p>720 x 480p x 59.94 Hz，高宽比比4:3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>720 x 480p x 59.94 Hz，高宽比比16:9</p></td>
<td align="left"><p>720 x 480p x 59.94 Hz，高宽比比16:9</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>1280 x 720p x 59.94 Hz，高宽比比16:9</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>1920 x1080i x 59.94 Hz，高宽比比16:9</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>1920 x 1080p x 59.94 Hz，高宽比比16:9</p></td>
</tr>
</tbody>
</table>

 

**50Hz DTV 系统：**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DTV 格式</th>
<th align="left">HDTV 格式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>640 x 480p x 59.94 Hz，高宽比比4:3</p></td>
<td align="left"><p>640 x 480p x 59.94 Hz，高宽比比4:3</p></td>
</tr>
<tr class="even">
<td align="left"><p>720（1440） x 576i x 50Hz，宽高比4:3</p></td>
<td align="left"><p>720（1440） x 576i x 50Hz，宽高比4:3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>720（1440） x 576i x 50Hz，宽高比16:9</p></td>
<td align="left"><p>720（1440） x 576i x 50Hz，宽高比16:9</p></td>
</tr>
<tr class="even">
<td align="left"><p>720 x 576p x 50Hz，纵横比4:3</p></td>
<td align="left"><p>720x 576p x 50Hz，宽高比4:3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>720 x 576p x 50Hz，纵横比16:9</p></td>
<td align="left"><p>720x 576p x 50Hz，宽高比16:9</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>1280 x 720p x 50Hz，高宽比比16:9</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>1920 x 1080i x 50Hz，纵横比16:9</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>1920 x 1080p x 50Hz，高宽比比16:9</p></td>
</tr>
</tbody>
</table>

 

为 Windows Vista 编写的微型端口驱动程序应继续符合[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)自动测试图形-0043，并添加这些表中指定的附加 DTV 模式。 为 Windows 7 编写的驱动程序只需支持新的**pfnGetAdditionalMonitorModeSet**和**pfnReleaseAdditionalMonitorModeSet**函数。


 
## <a name="see-also"></a>另请参阅

[确定显示适配器是否支持 VidPN](determining-whether-a-vidpn-is-supported-on-a-display-adapter.md)

[枚举 Cofunctional VidPN 源和目标模式](enumerating-cofunctional-vidpn-source-and-target-modes.md)

[视频呈现网络术语](video-present-network-terminology.md)

[VidPN 对象和接口](vidpn-objects-and-interfaces.md)