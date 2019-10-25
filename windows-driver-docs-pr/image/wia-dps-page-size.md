---
title: WIA\_DPS\_页\_大小
description: WIA\_DPS\_页\_大小属性包含当前选定要扫描的页的大小。
ms.assetid: 16e32b83-26b8-4283-a937-9fbbe77b42b8
keywords:
- WIA_DPS_PAGE_SIZE 图像设备
topic_type:
- apiref
api_name:
- WIA_DPS_PAGE_SIZE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d993a8a2c32659d715aeb61cd944d3791ede2f41
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840717"
---
# <a name="wia_dps_page_size"></a>WIA\_DPS\_页\_大小


WIA\_DPS\_页\_大小属性包含当前选定要扫描的页的大小。

## <span id="ddk_wia_dps_page_size_si"></span><span id="DDK_WIA_DPS_PAGE_SIZE_SI"></span>


属性类型： VT\_I4

有效值： WIA\_的\_列表

访问权限：读/写

<a name="remarks"></a>备注
-------

若要选择要扫描的页的维度，应用程序会将 WIA\_DPS\_页\_大小。 WIA 微型驱动程序创建并维护此属性。

下表描述了在[**WIA\_IPS\_页\_大小**](wia-ips-page-size.md)中有效的常量。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_PAGE_A4</p></td>
<td><p>页面大小为8267×11692（纵向）。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PAGE_CUSTOM</p></td>
<td><p>页面大小由<a href="wia-dps-page-height.md" data-raw-source="[&lt;strong&gt;WIA_DPS_PAGE_HEIGHT&lt;/strong&gt;](wia-dps-page-height.md)"><strong>WIA_DPS_PAGE_HEIGHT</strong></a>和<a href="wia-dps-page-width.md" data-raw-source="[&lt;strong&gt;WIA_DPS_PAGE_WIDTH&lt;/strong&gt;](wia-dps-page-width.md)"><strong>WIA_DPS_PAGE_WIDTH</strong></a>属性的值来定义。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PAGE_LETTER</p></td>
<td><p>页面大小为8500×11000（纵向）。</p></td>
</tr>
</tbody>
</table>

 

[**WIA\_IPS\_方向**](wia-ips-orientation.md)属性的值确定当前所选页面的方向。 WIA\_DPS\_页\_宽度和 WIA\_DPS\_页\_高度属性报告页面的尺寸，以英寸（001）为单位。 这些属性的值必须与[**wia\_ips\_XEXTENT**](wia-ips-xextent.md)和[**wia\_ips\_YEXTENT**](wia-ips-yextent.md)属性（以像素为单位）中的值相同。

WIA\_属性\_列表类型值应依赖于 WIA\_IP\_方向属性的有效设置。 如果设备无法使用 WIA\_页面\_A4 设置来扫描面向横向的文档，则 wia\_页\_A4 不应出现在 wia\_DP\_页的有效值列表中。\_IP\_方向设置为 LANSCAPE。

如果应用程序将 WIA\_DPS\_页面\_大小设置为 WIA\_页面\_自定义以外的任何值，则微型驱动程序应调整 WIA\_DPS\_\_WIDTH and WIA 的值\_DPS\_页面\_高度，以英寸（001）的千分之几个页面的尺寸。 微型驱动程序还应将 WIA\_IPS\_XEXTENT 和 WIA\_IP\_YEXTENT 的值调整为以像素为单位的。

如果扩展盘区设置（WIA\_IPS\_XEXTENT 或 WIA\_IPS\_YEXTENT）更改为与当前页面大小设置*不*匹配的值，则微型驱动程序应更改 WIA\_DPS\_页的值\_SIZE 属性到 WIA\_页面\_自定义。 微型驱动程序还应根据新的区设置来修改 WIA\_DPS\_页面\_宽度或 WIA\_DP\_的高度。

如果 WIA\_IP\_方向设置为 LANSCAPE，则区设置将为 "翻转"。 例如，如果应用程序将 WIA\_DPS\_页面\_大小设置为 WIA\_页面\_A4，则微型驱动程序应将 WIA\_DP\_\_WIDTH 设置为11692，WIA\_DP\_页\_高度为8267。 （微型驱动程序还应\_IP\_YEXTENT 设置 WIA\_IPS\_XEXTENT 和 WIA。）请注意，如果 WIA\_DPS\_页面\_大小设置为 WIA\_页面\_自定义，则不会使用方向设置来确定要扫描的页面的范围维度。

微型驱动程序必须确保 WIA\_IP\_方向属性与当前选择区域一致。 如果应用程序将 "WIA\_IP\_方向" 的值更改为对当前所选页面大小无效的值，则微型驱动程序应将 "WIA\_\_\_"新的方向值。

如果应用程序将 WIA\_DPS\_"\_大小" 属性设置为 "WIA\_" 页\_"自定义"，则不会影响当前选定区域。 WIA 微型驱动程序应从[**WIA\_ips\_XPOS**](wia-ips-xpos.md)和[**WIA\_ip\_YPOS**](wia-ips-ypos.md)属性的当前设置开始，获取当前的图像布局。 如果页面大小设置导致扫描仪平台之外的选择区域，则微型驱动程序必须自动将 WIA\_IP\_XPOS 和 WIA\_\_IPS 的值调整为有效设置。 如果 WIA\_DPS\_页\_大小和 WIA\_IP\_方向属性同时设置，并且它们在组合应用时无效，则微型驱动程序应通过返回[**IWiaMiniDrv：:D rvvalidateitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)方法错误。

以下四个代码示例显示了以下 WIA\_DPS\_页面\_大小方案：

1.  驱动程序报告设置。

2.  应用程序将 WIA\_DPS\_页面\_大小属性设置为 WIA\_页面\_字母。

3.  应用程序将[**WIA\_ip\_方向**](wia-ips-orientation.md)属性设置为 LANSCAPE。

4.  应用程序将[**WIA\_IPS\_XEXTENT**](wia-ips-xextent.md)属性更改为较小的值。

**示例1：微型驱动程序报告设置**

在下面的代码示例中，微型驱动程序在应用程序设置任何 WIA 属性之前设置自定义选择区域。 在这种情况下，选择区域表示整个平台。

WIA_DPS_PAGE_SIZE = WIA_PAGE_CUSTOM WIA_DPS_PAGE_WIDTH = 11500 WIA_DPS_PAGE_HEIGHT = 14000 WIA_IPS_ORIENTATION = WIA_IPS_XPOS WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 0 WIA_IPS_YEXTENT = 1150 WIA_IPS_XRES = 1400 WIA_IPS_YRES = 100 = 100

**示例2：应用程序将 WIA\_DPS\_页面\_大小属性设置为 WIA\_页面\_字母**

WIA_DPS_PAGE_SIZE = WIA_PAGE_LETTER WIA_DPS_PAGE_WIDTH = 8500 WIA_DPS_PAGE_HEIGHT = 11000 WIA_IPS_ORIENTATION = WIA_IPS_XPOS WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 0 WIA_IPS_YEXTENT = 850 WIA_IPS_XRES = 1100 WIA_IPS_YRES = 100 = 100

**示例3：应用程序将 WIA\_IPS\_方向属性设置为 LANSCAPE**

物理平台必须能够获取最初处于横向方向的页面。

WIA_DPS_PAGE_SIZE = WIA_PAGE_LETTER WIA_DPS_PAGE_HEIGHT = 11000 WIA_DPS_PAGE_WIDTH = 8500 WIA_IPS_ORIENTATION = LANSCAPE WIA_IPS_XPOS = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 1100 WIA_IPS_YEXTENT = 850 WIA_IPS_XRES = 100 WIA_IPS_YRES = 100

**示例4：应用程序将 WIA\_IPS\_XEXTENT 属性更改为较小值**

在下面的代码示例中，应用程序将 WIA\_IPS\_XEXTENT 属性更改为1000。 微型驱动程序应假定 WIA\_IPS\_XEXTENT 的新值对 WIA\_DPS\_页面\_大小属性不再有效，因此应将 WIA\_DPS\_\_大小对于 WIA\_页面\_自定义。 微型驱动程序还必须[ **\_DPS\_页面\_宽度调整 WIA**](wia-dps-page-width.md)。

WIA_DPS_PAGE_SIZE = WIA_PAGE_CUSTOM WIA_DPS_PAGE_HEIGHT = 10000 WIA_DPS_PAGE_WIDTH = 8500 WIA_IPS_ORIENTATION = LANSCAPE WIA_IPS_XPOS = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 1000 WIA_IPS_YEXTENT = 850 WIA_IPS_XRES = 100 WIA_IPS_YRES = 100

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>适用于 Microsoft Windows XP。 对于 Windows Vista 和更高版本，请使用完全相同的 WIA_IPS_PAGE_SIZE 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef （包括 Wiadef）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**IWiaMiniDrv：:d rvValidateItemProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)

[**WIA\_DPS\_页\_高度**](wia-dps-page-height.md)

[**WIA\_DPS\_页\_大小**](wia-dps-page-size.md)

[**WIA\_DPS\_页\_宽度**](wia-dps-page-width.md)

[**WIA\_IP\_方向**](wia-ips-orientation.md)

[**WIA\_IP\_页\_大小**](wia-ips-page-size.md)

[**WIA\_IP\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IP\_XPOS**](wia-ips-xpos.md)

[**WIA\_IP\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IP\_YPOS**](wia-ips-ypos.md)
