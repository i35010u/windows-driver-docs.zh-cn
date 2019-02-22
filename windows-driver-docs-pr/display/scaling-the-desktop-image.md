---
title: 扩展桌面映像
description: 扩展桌面映像
ms.assetid: e27c7510-45b0-46e6-878f-b901cdd1cd57
keywords:
- 连接显示 WDK Windows 7 显示，CCD 概念，缩放桌面映像
- 连接显示 WDK Windows Server 2008 R2 显示，CCD 概念，缩放桌面映像
- 配置显示 WDK Windows 7 显示，CCD 概念，缩放桌面映像
- 配置显示 WDK Windows Server 2008 R2 显示，CCD 概念，缩放桌面映像
- CCD 概念 WDK Windows 7 的显示，缩放桌面映像
- 显示 CCD 概念 WDK Windows Server 2008 R2，请缩放桌面映像
- 扩展桌面映像 WDK Windows 7 显示
- 扩展桌面映像 WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 545000757901bb9a6b6002447fa62bbc684a7d78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541094"
---
# <a name="scaling-the-desktop-image"></a>扩展桌面映像


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

可以使用调用方[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533) CCD 函数来扩展桌面映像到监视器。 如果桌面和监视器都使用相同的分辨率**SetDisplayConfig**不需要将桌面图像缩放为监视器。 这**SetDisplayConfig**操作称为标识缩放。 如果不同，桌面和监视器的分辨率**SetDisplayConfig**适用以下类型的扩展之一。 由定义监视器分辨率[ **DISPLAYCONFIG\_目标\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff553993)结构。

<span id="Centered"></span><span id="centered"></span><span id="CENTERED"></span>**居中**  
居中缩放是一种模式在其中桌面显示在监视器不包含任何缩放根本。 当[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)适用居中缩放黑带区可能在上方和下方在桌面上可见。 下图显示了居中缩放。

![缩放图阐释居中](images/ccd-center-scale.png)

<span id="Stretched"></span><span id="stretched"></span><span id="STRETCHED"></span>**拉伸**  
外延式缩放是一种模式中的桌面的水平和垂直拉伸以确保使用整个显示器的监视器。 当[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)适用拉伸缩放，没有黑色选择带是可见的上方和下方桌面。 但是，桌面可能会出现失真。 下图显示了外延式缩放。

![图阐释拉伸缩放](images/ccd-stretch-scale.png)

<span id="Aspect-Ratio-Preserving_Stretched"></span><span id="aspect-ratio-preserving_stretched"></span><span id="ASPECT-RATIO-PRESERVING_STRETCHED"></span>**纵横比保留拉伸**  
纵横比保留外延式缩放是桌面处于外延式水平和垂直尽可能多地同时保持纵横比的模式。 时[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)适用长宽比保留外延式缩放，黑色的带区可能会显示也*上方和下方*或*左和右侧的*桌面。 但是，黑色的带区不能为可见两者*上方和下方*并*左侧和右侧的*桌面。 用户应为首选这种类型的扩展，因为**SetDisplayConfig**适用这种缩放为默认值。 下图显示了保留纵横比外延式缩放。

![图阐释长宽比保留外延式缩放](images/ccd-arpstretch-scale.png)

缩放取决于用于路径的源和目标模式。 此外，可以调用调用方[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)而无需指定目标模式信息 (即，设置*modeInfoArray*参数是可选的和可以将设置为**NULL**)。 因此，调用方不能如果通常预测**SetDisplayConfig**必须执行任何缩放。 此外，不存在 API 获取缩放图形适配器支持的类型的完整列表。 [ **EnumDisplaySettings** ](https://msdn.microsoft.com/library/windows/desktop/dd162611) （Windows SDK 文档中所述） 的 Win32 函数返回 DMDFO\_中的默认值**dmDisplayFixedOutput**成员**DEVMODE**结构的*lpDevMode*参数指向调用方时请求新的 Windows 7 缩放类型。

调用方传递到网站的规模[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)是缩放目的而不是显式请求执行缩放操作。 如果需要缩放 （例如，源和目标分辨率不同） **SetDisplayConfig**使用调用方提供的缩放。 如果不支持提供的缩放，则**SetDisplayConfig**使用图形适配器的默认缩放。 当源和目标的解决方法的调用方传递到**SetDisplayConfig**是相同的**SetDisplayConfig**始终集确定缩放。

下表显示了不同[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)缩放请求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">符号表中</th>
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
<p>目前，在平板电脑系统中，默认值被拉伸。 图形适配器支持在具有非平板电脑系统上<a href="windows-vista-display-driver-model-design-guide.md" data-raw-source="[Windows Display Driver Model (WDDM)](windows-vista-display-driver-model-design-guide.md)">Windows 显示器驱动程序模型 (WDDM)</a>，由驱动程序定义默认值。 支持 Windows 显示驱动程序模型 (WDDM) 使用的图形适配器在具有非平板电脑系统上<a href="https://msdn.microsoft.com/library/windows/hardware/ff557343" data-raw-source="[features new for Windows 7](https://msdn.microsoft.com/library/windows/hardware/ff557343)">适用于 Windows 7 新功能</a>，默认值是 DC_ASPECTRATIOCENTEREDMAX。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DatabaseValue</p></td>
<td align="left"><p>当前已连接监视器的数据库中的缩放值</p></td>
</tr>
</tbody>
</table>

 

下表显示了在数据库中保存的值和实际设置的值。

缩放标志传递给 SetDisplayConfig 生成源模式和目标模式的结果源模式和目标模式具有不同的解决方法具有相同的分辨率**设置**

**应用商店**

**Set**

**应用商店**

DC\_标识不在 Db 中的当前配置

DC\_标识

AdapterDefault

AdapterDefault

AdapterDefault

DC\_Db 中的标识当前配置

DC\_标识

DatabaseValue

DatabaseValue

DatabaseValue

DC\_居中

DC\_标识

DC\_居中

DC\_居中

DC\_居中

DC\_STRETCHED

DC\_标识

DC\_STRETCHED

DC\_STRETCHED

DC\_STRETCHED

DC\_上使用 Windows 7 功能驱动程序的 WDDM ASPECTRATIOCENTEREDMAX

DC\_标识

DC\_ASPRATIOMAX

DC\_ASPRATIOMAX

DC\_ASPRATIOMAX

DC\_ASPECTRATIOCENTEREDMAX WDDM 驱动程序

DC\_标识

AdapterDefault

AdapterDefault

AdapterDefault

DC\_WDDM 上使用 Windows 7 功能驱动程序支持自定义缩放在路径上自定义

DC\_自定义

DC\_自定义

DC\_自定义

DC\_自定义

DC\_WDDM 上不支持自定义缩放在路径的 Windows 7 功能驱动程序与自定义

DC\_标识

AdapterDefault

AdapterDefault

AdapterDefault

DC\_WDDM 驱动程序上自定义

DC\_标识

AdapterDefault

AdapterDefault

AdapterDefault

DC\_首选不在 Db 中的当前配置

DC\_标识

AdapterDefault

AdapterDefault

AdapterDefault

DC\_首选 Db 中的当前配置

DC\_标识

DatabaseValue

DatabaseValue

DatabaseValue

 

下表显示了如何缩放调用方可以将传递到旧[ **ChangeDisplaySettingsEx**](https://msdn.microsoft.com/library/windows/desktop/dd183413)API （Windows SDK 文档中所述） 映射到缩放集。

缩放标志传递给 ChangeDisplaySettingsEx 生成源模式和目标模式的结果源模式和目标模式具有不同的解决方法具有相同的分辨率**设置**

**应用商店**

**Set**

**应用商店**

DMDFO\_不 CCD 数据库中的当前配置的默认值

DC\_标识

AdapterDefault

AdapterDefault

AdapterDefault

DMDFO\_CCD 数据库中的当前配置的默认值

DC\_标识

DatabaseValue

DatabaseValue

DatabaseValue

DMDFO\_STRETCH

DC\_标识

DC\_STRETCHED

DC\_STRETCHED

DC\_STRETCHED

DMDFO\_CENTER

DC\_标识

DC\_居中

DC\_居中

DC\_居中

DM\_DISPLAYFIXEDOUTPUT 未设置，不 CCD 数据库中的当前配置

DC\_标识

AdapterDefault

AdapterDefault

AdapterDefault

DM\_DISPLAYFIXEDOUTPUT 未设置，CCD 数据库中的当前配置

DC\_标识

DatabaseValue

DatabaseValue

DatabaseValue

 

下表显示如何显示配置缩放转换并返回从[ **EnumDisplaySettings**](https://msdn.microsoft.com/library/windows/desktop/dd162611)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">当前活动缩放</th>
<th align="left">GDI 缩放从旧 EnumDIsplaySettings(ENUM_CURRENT_SETTINGS) 返回值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DC_IDENTITY</p></td>
<td align="left"><p>DMDFO_DEFAULT</p></td>
</tr>
<tr class="even">
<td align="left"><p>DC_CENTERED</p></td>
<td align="left"><p>DMDFO_CENTER，从而</p></td>
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

 

### <a name="span-iddirectxgamesandscalingspanspan-iddirectxgamesandscalingspandirectx-games-and-scaling"></a><span id="directx_games_and_scaling"></span><span id="DIRECTX_GAMES_AND_SCALING"></span>DirectX 游戏和缩放

Microsoft DirectX 9 L 和更早运行时需要应用程序始终调用[ **ChangeDisplaySettingsEx** ](https://msdn.microsoft.com/library/windows/desktop/dd183413)函数，没有 DM\_中设置 DISPLAYFIXEDOUTPUT **dmFields**成员的 DEVMODE 结构*lpDevMode*参数指向。 DirectX 10 和更高版本的运行时允许应用程序以选择缩放这些应用程序传递给**ChangeDisplaySettingsEx**。 下表显示了缩放比例标志传递到值的映射**ChangeDisplaySettingsEx**。

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
<td align="left"><p>DMDFO_DEFAULT、 DMDFO_CENTER 或 DMDFO_STRETCH。 缩放应用程序使用依赖于若干因素，包括当前桌面缩放和驱动程序公开的模式列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGI_MODE_SCALING_CENTERED</p></td>
<td align="left"><p>DMDFO_CENTER，从而</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXGI_MODE_SCALING_STRETCHED</p></td>
<td align="left"><p>DMDFO_STRETCH</p></td>
</tr>
</tbody>
</table>

 

通过使用此信息与前面的缩放性表结合使用，可以确定从 DirectX 应用程序的预期缩放。

 

 





