---
title: 缩放桌面图像
description: 缩放桌面图像
ms.assetid: e27c7510-45b0-46e6-878f-b901cdd1cd57
keywords:
- 连接显示 WDK Windows 7 显示、CCD 概念、缩放桌面映像
- 连接显示 WDK Windows Server 2008 R2 显示、CCD 的概念、缩放桌面映像
- 配置显示 WDK Windows 7 显示、CCD 概念、缩放桌面映像
- 配置显示 WDK Windows Server 2008 R2 显示、CCD 概念、缩放桌面映像
- CCD 概念 WDK Windows 7 显示，缩放桌面映像
- CCD 概念 WDK Windows Server 2008 R2 显示，缩放桌面映像
- 缩放桌面图像 WDK Windows 7 显示
- 缩放桌面映像 WDK Windows Server 2008 R2 显示器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40bb5343081aae629bb0ff2e19edfde70f016565
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104648"
---
# <a name="scaling-the-desktop-image"></a>缩放桌面图像


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

调用方可以使用 [**SetDisplayConfig**](/windows/desktop/api/winuser/nf-winuser-setdisplayconfig) CCD 函数将桌面映像缩放到监视器。 如果桌面和监视器使用相同的分辨率，则不需要 **SetDisplayConfig** 将桌面映像缩放到监视器。 此 **SetDisplayConfig** 操作称为 "标识缩放"。 如果桌面和监视器分辨率不同， **SetDisplayConfig** 将应用以下一种缩放类型。 监视器分辨率由 [**DISPLAYCONFIG \_ 目标 \_ 模式**](/windows/desktop/api/wingdi/ns-wingdi-displayconfig_target_mode) 结构定义。

<span id="Centered"></span><span id="centered"></span><span id="CENTERED"></span>**界线**  
居中缩放是一种模式，在该模式下桌面显示在监视器上，根本不进行任何缩放。 当 [**SetDisplayConfig**](/windows/desktop/api/winuser/nf-winuser-setdisplayconfig) 应用居中缩放时，黑色带区可能在桌面的上方和下方可见。 下图显示了中心缩放。

![阐释中心缩放的图](images/ccd-center-scale.png)

<span id="Stretched"></span><span id="stretched"></span><span id="STRETCHED"></span>**扩展**  
拉伸缩放是一种模式，在该模式下，桌面在监视器上水平和垂直拉伸，以确保使用整个显示。 当 [**SetDisplayConfig**](/windows/desktop/api/winuser/nf-winuser-setdisplayconfig) 应用延伸缩放时，桌面上方和下方不会显示黑色带区。 但是，桌面可能会失真。 下图显示了延伸缩放。

![演示拉伸缩放的图](images/ccd-stretch-scale.png)

<span id="Aspect-Ratio-Preserving_Stretched"></span><span id="aspect-ratio-preserving_stretched"></span><span id="ASPECT-RATIO-PRESERVING_STRETCHED"></span>**纵横比-保留延伸**  
纵横比-保留延伸缩放是一种模式，在该模式下，桌面会在保持纵横比的同时水平和垂直拉伸。 当 [**SetDisplayConfig**](/windows/desktop/api/winuser/nf-winuser-setdisplayconfig) 应用纵横比保留延伸缩放时，黑色带区可能会显示在桌面的 *上方和下方* 或 *左侧或右侧* 。 但是，黑色带区不能同时*显示在桌面的**上方和下方*。 由于用户需要使用这种类型的缩放，因此 **SetDisplayConfig** 会将此类型的缩放作为默认值应用。 下图显示了纵横比，其中保留了延伸缩放。

![图说明了纵横比-保留延伸比例](images/ccd-arpstretch-scale.png)

缩放取决于用于路径的源和目标模式。 此外，调用方可以调用 [**SetDisplayConfig**](/windows/desktop/api/winuser/nf-winuser-setdisplayconfig) 而无需指定目标模式信息 (即，将 *modeInfoArray* 参数设置为可选，并且可以将其设置为 **NULL**) 。 因此，调用方通常无法预测 **SetDisplayConfig** 是否必须执行任何缩放。 此外，不存在 API 来获取图形适配器支持的缩放类型的完整列表。 Windows SDK) 文档中所述的[**EnumDisplaySettings**](/windows/desktop/api/winuser/nf-winuser-enumdisplaysettingsa) Win32 函数 (在 \_ 调用方请求新的 Windows 7 缩放**DEVMODE**类型时*lpDevMode*参数指向的**dmDisplayFixedOutput**成员中返回 DMDFO 默认值。

调用方传递给 [**SetDisplayConfig**](/windows/desktop/api/winuser/nf-winuser-setdisplayconfig) 的缩放是缩放意向，而不是显式请求来执行缩放操作。 如果需要缩放 (例如，源和目标解析) 不同， **SetDisplayConfig** 将使用调用方提供的缩放。 如果不支持所提供的缩放， **SetDisplayConfig** 将使用图形适配器的默认缩放。 当调用方传递给 **SetDisplayConfig** 的源和目标解析相同时， **SetDisplayConfig** 始终设置标识缩放。

下表显示了不同的 [**SetDisplayConfig**](/windows/desktop/api/winuser/nf-winuser-setdisplayconfig) 缩放请求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">表中的符号</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DC_IDENTITY</p></td>
<td align="left"><p>DISPLAYCONFIG_SCALING_IDENTITY</p></td>
</tr>
<tr class="even">
<td align="left"><p>DC_CENTERED</p></td>
<td align="left"><p>DISPLAYCONFIG_SCALING_CENTERED</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DC_STRETCHED</p></td>
<td align="left"><p>DISPLAYCONFIG_SCALING_STRETCHED</p></td>
</tr>
<tr class="even">
<td align="left"><p>DC_ASPECTRATIOCENTEREDMAX</p></td>
<td align="left"><p>DISPLAYCONFIG_SCALING_ASPECTRATIOCENTEREDMAX</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DC_CUSTOM</p></td>
<td align="left"><p>DISPLAYCONFIG_SCALING_CUSTOM</p></td>
</tr>
<tr class="even">
<td align="left"><p>DC_PREFERRED</p></td>
<td align="left"><p>DISPLAYCONFIG_SCALING_PREFERRED</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AdapterDefault</p></td>
<td align="left"><p>适配器默认缩放值</p>
<p>目前，tablet 系统上的默认值为 "拉伸"。 在支持 <a href="windows-vista-display-driver-model-design-guide.md" data-raw-source="[Windows Display Driver Model (WDDM)](windows-vista-display-driver-model-design-guide.md)">Windows 显示驱动程序模型 (WDDM) </a>的非平板系统上，默认值是由驱动程序定义的。 在具有支持 Windows 显示驱动程序模型的图形适配器的非平板系统上 (WDDM) ，其 <a href="/windows-hardware/drivers/what-s-new-in-driver-development" data-raw-source="[features new for Windows 7](../what-s-new-in-driver-development.md)">功能为 windows 7</a>，默认值为 DC_ASPECTRATIOCENTEREDMAX。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DatabaseValue</p></td>
<td align="left"><p>当前连接的监视器的数据库的缩放值</p></td>
</tr>
</tbody>
</table>

 

下表显示了保存在数据库中的值和实际设置的值。

传递给 SetDisplayConfig 的缩放标志生成的源模式和目标模式具有相同的分辨率。结果源模式和目标模式具有不同的分辨率 **集**

**Store**

**设置**

**Store**

DC \_ 标识当前未在 Db 中的配置

DC \_ 标识

AdapterDefault

AdapterDefault

AdapterDefault

\_数据库中的 DC 标识当前配置

DC \_ 标识

DatabaseValue

DatabaseValue

DatabaseValue

DC \_ 居中

DC \_ 标识

DC \_ 居中

DC \_ 居中

DC \_ 居中

DC 已 \_ 拉伸

DC \_ 标识

DC 已 \_ 拉伸

DC 已 \_ 拉伸

DC 已 \_ 拉伸

\_包含 Windows 7 功能驱动程序的 WDDM 上的 DC ASPECTRATIOCENTEREDMAX

DC \_ 标识

DC \_ ASPRATIOMAX

DC \_ ASPRATIOMAX

DC \_ ASPRATIOMAX

\_WDDM 驱动程序上的 DC ASPECTRATIOCENTEREDMAX

DC \_ 标识

AdapterDefault

AdapterDefault

AdapterDefault

\_具有 Windows 7 功能驱动程序的在 WDDM 上自定义的自定义支持路径上的自定义缩放

DC \_ 自定义

DC \_ 自定义

DC \_ 自定义

DC \_ 自定义

\_在具有 Windows 7 功能驱动程序的 WDDM 上自定义，不支持路径上的自定义缩放

DC \_ 标识

AdapterDefault

AdapterDefault

AdapterDefault

\_WDDM 驱动程序上的 DC 自定义

DC \_ 标识

AdapterDefault

AdapterDefault

AdapterDefault

DC \_ 首选当前配置不在数据库中

DC \_ 标识

AdapterDefault

AdapterDefault

AdapterDefault

\_数据库中的 DC 首选当前配置

DC \_ 标识

DatabaseValue

DatabaseValue

DatabaseValue

 

下表显示了调用方可以如何传递到旧的 [**ChangeDisplaySettingsEx**](/windows/desktop/api/winuser/nf-winuser-changedisplaysettingsexa)API 的缩放 (Windows SDK 文档) 映射到缩放集。

传递给 ChangeDisplaySettingsEx 的缩放标志生成的源模式和目标模式具有相同的分辨率。结果源模式和目标模式具有不同的分辨率 **集**

**Store**

**设置**

**Store**

DMDFO \_ 默认值与当前配置不在 CCD 数据库中

DC \_ 标识

AdapterDefault

AdapterDefault

AdapterDefault

DMDFO \_ 默认为 CCD 数据库中的当前配置

DC \_ 标识

DatabaseValue

DatabaseValue

DatabaseValue

DMDFO \_ STRETCH

DC \_ 标识

DC 已 \_ 拉伸

DC 已 \_ 拉伸

DC 已 \_ 拉伸

DMDFO \_ 中心

DC \_ 标识

DC \_ 居中

DC \_ 居中

DC \_ 居中

\_未设置 DM DISPLAYFIXEDOUTPUT，当前配置未在 CCD 数据库中

DC \_ 标识

AdapterDefault

AdapterDefault

AdapterDefault

DM \_ DISPLAYFIXEDOUTPUT 未设置，CCD 数据库中的当前配置

DC \_ 标识

DatabaseValue

DatabaseValue

DatabaseValue

 

下表显示了如何从 [**EnumDisplaySettings**](/windows/desktop/api/winuser/nf-winuser-enumdisplaysettingsa)转换和返回显示配置缩放。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">当前活动缩放</th>
<th align="left">从旧的 EnumDIsplaySettings (ENUM_CURRENT_SETTINGS 返回的 GDI 缩放值) </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DC_IDENTITY</p></td>
<td align="left"><p>DMDFO_DEFAULT</p></td>
</tr>
<tr class="even">
<td align="left"><p>DC_CENTERED</p></td>
<td align="left"><p>DMDFO_CENTER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DC_STRETCHED</p></td>
<td align="left"><p>DMDFO_STRETCH</p></td>
</tr>
<tr class="even">
<td align="left"><p>DC_ASPRATIOMAX</p></td>
<td align="left"><p>DMDFO_DEFAULT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DC_CUSTOM</p></td>
<td align="left"><p>DMDFO_DEFAULT</p></td>
</tr>
<tr class="even">
<td align="left"><p>DC_PREFERRED</p></td>
<td align="left"><p>DMDFO_DEFAULT</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddirectx_games_and_scalingspanspan-iddirectx_games_and_scalingspandirectx-games-and-scaling"></a><span id="directx_games_and_scaling"></span><span id="DIRECTX_GAMES_AND_SCALING"></span>DirectX 游戏和缩放

Microsoft DirectX 9L 和更早的运行时要求应用程序始终调用[**ChangeDisplaySettingsEx**](/windows/desktop/api/winuser/nf-winuser-changedisplaysettingsexa)函数，而不是 \_ 在*LPDEVMODE*参数指向的 DEVMODE 结构的**dmFields**成员中设置 DM DISPLAYFIXEDOUTPUT。 DirectX 10 和更高版本的运行时允许应用程序选择这些应用程序传递给 **ChangeDisplaySettingsEx**的缩放。 下表显示了将缩放值映射到传递给 **ChangeDisplaySettingsEx**的缩放标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DXGI 翻转链缩放值</th>
<th align="left">传递给 ChangeDisplaySettingsEx 的缩放标志</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXGI_MODE_SCALING_UNSPECIFIED</p></td>
<td align="left"><p>DMDFO_DEFAULT、DMDFO_CENTER 或 DMDFO_STRETCH。 应用程序使用的缩放取决于多个因素，包括当前桌面缩放和驱动程序公开的模式列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGI_MODE_SCALING_CENTERED</p></td>
<td align="left"><p>DMDFO_CENTER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXGI_MODE_SCALING_STRETCHED</p></td>
<td align="left"><p>DMDFO_STRETCH</p></td>
</tr>
</tbody>
</table>

 

通过将此信息与前面的缩放表结合使用，可以确定 DirectX 应用程序所需的缩放。

