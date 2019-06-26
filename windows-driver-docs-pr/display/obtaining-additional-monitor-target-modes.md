---
title: 获取其他监视目标模式
description: 获取其他监视目标模式
ms.assetid: fc0e2d43-8fc2-4757-ba77-f72a01e04343
keywords:
- 监视目标模式 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9411b1974edde028566bf9bc30b8a608a1466f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372784"
---
# <a name="obtaining-additional-monitor-target-modes"></a>获取其他监视目标模式


从 Windows 7 开始，新的监视器界面不可用， [ **DXGK\_监视器\_接口\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_monitor_interface_v2)。 它提供了两个其他函数，不是在原始[ **DXGK\_监视器\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_monitor_interface)接口：

[**pfnGetAdditionalMonitorModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_getadditionalmonitormodeset)

[**pfnReleaseAdditionalMonitorModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_releaseadditionalmonitormodeset)

这些函数提供有关显示微型端口驱动程序，以将目标模式添加到 VidPN 目标的动态和可缩放方法。 相比之下，DXGK\_监视器\_接口接口提供了静态列表的目标模式。 使用这些函数，该驱动程序可以查询适用于其他模式，它应枚举的列表。 该驱动程序可以验证请求的模式，并拒绝这些监视器不支持。

当显示微型端口驱动程序收到对驱动程序实现调用[ **DxgkDdiEnumVidPnCofuncModality** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)函数合用来枚举目标模式

它应使用以下过程将兼容的计时信息添加到目标模式集：

1.  返回时，它调用它获取的已筛选的其他目标模式[ **pfnGetAdditionalMonitorModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_getadditionalmonitormodeset)。 它应返回常规目标模式中，如中所述[枚举同时正常工作 VidPN 源和目标模式](enumerating-cofunctional-vidpn-source-and-target-modes.md)。

2.  **PfnGetAdditionalMonitorModeSet**函数将返回以下：
    -   *ppAdditionalModesSet*，一系列中的额外计时模式[ **DXGK\_TARGETMODE\_详细信息\_计时**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgk_targetmode_detail_timing)格式。
    -   *pNumberModes，* 计时模式数。

3.  循环访问所有这些计时模式。

4.  筛选出所有不兼容的计时模式和已提供在调用任何常规模式*DxgkDdiEnumVidPnCofuncModality*。

5.  转换到剩余的计时模式[ **D3DKMDT\_VIDPN\_目标\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_target_mode)类型。

6.  将所有剩余的计时模式添加到 VidPN 目标模式集。

7.  调用[ **pfnReleaseAdditionalMonitorModeSet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_releaseadditionalmonitormodeset)释放从返回的额外计时模式列表**pfnGetAdditionalMonitorModeSet**。

显示微型端口驱动程序应将添加到 VidPN 源模式集和目标模式集的硬件支持的所有其他时间模式。 在显示模式下管理器 (DMM) 生成的模式列表，所有显示模式，包括由监视器不支持的额外计时模式表示为监视器不支持，并且只能在 raw 模式列表中出现。 而不管是否连接监视器是，微型端口驱动程序应报告所有 VidPN 源和目标模式集支持的监视器。 报表仅支持监视的模式的驱动程序还必须报告不受当前连接监视器的附加模式。

## <a name="crt-monitors"></a>CRT 监视器

对于 CRT 监视器 DMM 添加视频电子标准协会 (VESA) 规范中定义的计时的更多的目标模式 640 x 480 x 60 Hz 标准监视器*VESA 和行业标准和计算机显示的指导原则监视器计时版本 1.0*。

## <a name="dtv-and-hdtv-monitors"></a>数字电视和 HDTV 监视器

对于数字电视 （数字电视） 和高清晰电视 (HDTV) 监视器，DMM 将添加更多的目标模式为所有的标准数字电视模式所需的[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)自动测试图形-0043，在下面的示例所示表。 显示微型端口驱动程序应修剪显示硬件不支持的所有模式。

**59.95 Hz 数字电视系统：**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">数字电视格式</th>
<th align="left">高清晰度电视格式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>640 x 480 p x 59.94 Hz，纵横比为 4:3</p></td>
<td align="left"><p>640 x 480 p x 59.94 Hz，纵横比为 4:3</p></td>
</tr>
<tr class="even">
<td align="left"><p>720(1440) x 480i x 59.94 Hz，纵横比为 4:3</p></td>
<td align="left"><p>720(1440) x 480i x 59.94 Hz，纵横比为 4:3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>720(1440) x 480i x 游戏如果在 59.94 Hz，纵横比为 16:9</p></td>
<td align="left"><p>720(1440) x 480i x 游戏如果在 59.94 Hz，纵横比为 16:9</p></td>
</tr>
<tr class="even">
<td align="left"><p>720 x 480 p x 59.94 Hz，纵横比为 4:3</p></td>
<td align="left"><p>720 x 480 p x 59.94 Hz，纵横比为 4:3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>720 x 480 p x 59.94 Hz，纵横比为 16:9</p></td>
<td align="left"><p>720 x 480 p x 59.94 Hz，纵横比为 16:9</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>1280x720 p x 59.94 Hz，纵横比为 16:9</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>1920 x1080i x 59.94 Hz，纵横比为 16:9</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>1920 x 1080 p x 59.94 Hz，纵横比为 16:9</p></td>
</tr>
</tbody>
</table>

 

**50 Hz 数字电视系统：**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">数字电视格式</th>
<th align="left">高清晰度电视格式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>640 x 480 p x 59.94 Hz，纵横比为 4:3</p></td>
<td align="left"><p>640 x 480 p x 59.94 Hz，纵横比为 4:3</p></td>
</tr>
<tr class="even">
<td align="left"><p>720(1440) x 576i x 50 Hz，纵横比为 4:3</p></td>
<td align="left"><p>720(1440) x 576i x 50 Hz，纵横比为 4:3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>720(1440) x 576i x 50 Hz，纵横比为 16:9</p></td>
<td align="left"><p>720(1440) x 576i x 50 Hz，纵横比为 16:9</p></td>
</tr>
<tr class="even">
<td align="left"><p>720 x 576 p x 50 Hz，纵横比为 4:3</p></td>
<td align="left"><p>720 x 576 p x 50 Hz，纵横比为 4:3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>720 x 576 p x 50 Hz，纵横比为 16:9</p></td>
<td align="left"><p>720 x 576 p x 50 Hz，纵横比为 16:9</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>1280x720 p x 50 Hz，纵横比为 16:9</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>1920 x 1080i x 50 Hz，纵横比为 16:9</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>1920 x 1080 p x 50 Hz，纵横比为 16:9</p></td>
</tr>
</tbody>
</table>

 

微型端口驱动程序为 Windows Vista 应继续符合编写[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)自动测试图形 0043 并添加这些表中指定的其他数字电视模式。 针对 Windows 7 编写驱动程序只需支持的新**pfnGetAdditionalMonitorModeSet**并**pfnReleaseAdditionalMonitorModeSet**函数。


 
## <a name="see-also"></a>请参阅

[确定是否 VidPN 显示适配器上受支持](determining-whether-a-vidpn-is-supported-on-a-display-adapter.md)

[枚举同时正常工作 VidPN 源和目标模式](enumerating-cofunctional-vidpn-source-and-target-modes.md)

[视频存在网络术语](video-present-network-terminology.md)

[VidPN 对象和接口](vidpn-objects-and-interfaces.md)