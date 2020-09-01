---
title: WIA \_ DPS \_ 页面 \_ 大小
description: "\"WIA \\_ DPS \\_ 页面 \\_ 大小\" 属性包含当前选定要扫描的页面的大小。"
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
ms.openlocfilehash: 0e32ea3e47d3fc96c40bde748233a4ab95785c82
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190077"
---
# <a name="wia_dps_page_size"></a>WIA \_ DPS \_ 页面 \_ 大小


"WIA \_ DPS \_ 页面 \_ 大小" 属性包含当前选定要扫描的页面的大小。

## <span id="ddk_wia_dps_page_size_si"></span><span id="DDK_WIA_DPS_PAGE_SIZE_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>注解
-------

若要选择要扫描的页面的尺寸，应用程序会设置 WIA \_ DPS \_ 页面 \_ 大小。 WIA 微型驱动程序创建并维护此属性。

下表描述了对 [**WIA \_ ip \_ 页面 \_ 大小**](wia-ips-page-size.md)有效的常量。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_PAGE_A4</p></td>
<td><p>页面大小为8267× 11692 (纵向) 。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PAGE_CUSTOM</p></td>
<td><p>页大小由 <a href="wia-dps-page-height.md" data-raw-source="[&lt;strong&gt;WIA_DPS_PAGE_HEIGHT&lt;/strong&gt;](wia-dps-page-height.md)"><strong>WIA_DPS_PAGE_HEIGHT</strong></a> 的值和 <a href="wia-dps-page-width.md" data-raw-source="[&lt;strong&gt;WIA_DPS_PAGE_WIDTH&lt;/strong&gt;](wia-dps-page-width.md)"><strong>WIA_DPS_PAGE_WIDTH</strong></a> 属性定义。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PAGE_LETTER</p></td>
<td><p>页面大小为8500× 11000 (纵向) 。</p></td>
</tr>
</tbody>
</table>

 

" [**WIA \_ IPS \_ 方向**](wia-ips-orientation.md) " 属性的值确定当前所选页面的方向。 WIA \_ dps \_ 页面 \_ 宽度和 WIA \_ dps \_ 页面 \_ 高度属性报告页面的尺寸（以英寸的千分之几分之)  ( 001。 这些属性的值必须与 [**wia \_ ips \_ XEXTENT**](wia-ips-xextent.md) 和 [**wia \_ ips \_ YEXTENT**](wia-ips-yextent.md) 属性（以像素为单位）中的值相同。

WIA \_ \_ 属性列表-类型化的值应依赖于 "WIA ip 方向" 属性的有效设置 \_ \_ 。 如果设备无法使用 WIA 页面 A4 设置扫描面向横向的 \_ 文档 \_ ， \_ \_ \_ \_ \_ 当 wia \_ ip \_ 方向设置为 "LANSCAPE" 时，wia 页 a4 不应出现在 "wia DPS 页面大小" 属性的有效值列表中。

如果应用程序将 WIA \_ dps \_ 页面 \_ 大小设置为 wia \_ 页面 \_ 自定义以外的任何值，则微型驱动程序应将 WIA \_ dps \_ 页面 \_ 宽度和 wia dps 页面高度的值调整 \_ \_ \_ 到页面的尺寸，以英寸 ( 001) 。 微型驱动程序还应将 WIA \_ ip \_ XEXTENT 和 wia ips YEXTENT 的值 \_ 调整 \_ 到页面的尺寸（以像素为单位）。

如果 (WIA \_ ip \_ XEXTENT 或 wia \_ ips YEXTENT) 的区设置 \_ 更改为与当前页面大小设置 *不* 匹配的值，则微型驱动程序应将 "wia \_ DPS 页面大小" 属性的值更改 \_ 为 " \_ wia \_ 页面 \_ 自定义"。 微型驱动程序还应 \_ \_ \_ \_ \_ \_ 根据新的范围设置来修改 wia dps 页面宽度或 wia dps 页面高度。

如果 WIA \_ ip \_ 方向设置为 LANSCAPE，则区设置将为 "翻转"。 例如，如果应用程序将 WIA \_ dps \_ 页面大小设置 \_ 为 wia \_ 页面 \_ A4，则微型驱动程序应将 wia \_ dps \_ 页面 \_ 宽度设置为11692，并将 wia \_ dps \_ 页面高度设置 \_ 为8267。  (微型驱动程序还应 \_ 相应地设置 WIA ip \_ XEXTENT 和 wia \_ ip \_ YEXTENT。 ) 请注意，如果 wia \_ DPS \_ 页面 \_ 大小设置为 wia \_ 页面 \_ 自定义，则不会使用方向设置来确定要扫描的页面的范围维度。

微型驱动程序必须确保 WIA \_ IPS \_ 方向属性与当前选择区域一致。 如果应用程序将 "WIA IPS 方向" 的值更改 \_ \_ 为对当前所选页面大小无效的值，则微型驱动程序应将 "wia DPS 页面大小" 的值更改 \_ \_ \_ 为新方向值所支持的页面大小。

如果应用程序将 "WIA \_ DPS \_ 页面 \_ 大小" 属性设置为 \_ "wia 页面 \_ 自定义"，则当前选择区域不受影响。 WIA 微型驱动程序应从 [**wia \_ ip \_ XPOS**](wia-ips-xpos.md) 和 [**wia \_ ip \_ YPOS**](wia-ips-ypos.md) 属性的当前设置开始，获取当前的图像布局。 如果页面大小设置导致扫描仪平台之外的选择区域，则微型驱动程序必须自动将 WIA \_ ip \_ XPOS 和 wia ips 属性的值调整 \_ \_ 为有效设置。 如果 WIA \_ DPS \_ 页面 \_ 大小和 wia \_ IPS \_ 方向属性同时设置并且它们在组合应用时无效，则微型驱动程序应通过在 [**IWiaMiniDrv：:d rvvalidateitemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties) 方法中返回错误来使应用程序的设置失败。

以下四个代码示例显示了以下 WIA \_ DPS \_ 页面 \_ 大小方案：

1.  驱动程序报告设置。

2.  应用程序将 "WIA \_ DPS \_ 页面 \_ 大小" 属性设置为 "wia \_ 页面 \_ 字母"。

3.  应用程序将 " [**WIA \_ ip \_ 方向**](wia-ips-orientation.md) " 属性设置为 "LANSCAPE"。

4.  应用程序会将 [**WIA \_ IPS \_ XEXTENT**](wia-ips-xextent.md) 属性更改为较小的值。

**示例1：微型驱动程序报告设置**

在下面的代码示例中，微型驱动程序在应用程序设置任何 WIA 属性之前设置自定义选择区域。 在这种情况下，选择区域表示整个平台。

WIA_DPS_PAGE_SIZE = WIA_PAGE_CUSTOM WIA_DPS_PAGE_WIDTH = 11500 WIA_DPS_PAGE_HEIGHT = 14000 WIA_IPS_ORIENTATION = 纵向 WIA_IPS_XPOS = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 1150 WIA_IPS_YEXTENT = 1400 WIA_IPS_XRES = 100 WIA_IPS_YRES = 100

**示例2：应用程序将 "WIA \_ DPS \_ 页面 \_ 大小" 属性设置为 "wia" \_ 页面 \_ 字母**

WIA_DPS_PAGE_SIZE = WIA_PAGE_LETTER WIA_DPS_PAGE_WIDTH = 8500 WIA_DPS_PAGE_HEIGHT = 11000 WIA_IPS_ORIENTATION = 纵向 WIA_IPS_XPOS = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 850 WIA_IPS_YEXTENT = 1100 WIA_IPS_XRES = 100 WIA_IPS_YRES = 100

**示例3：应用程序将 WIA \_ ip \_ 方向属性设置为 LANSCAPE**

物理平台必须能够获取最初处于横向方向的页面。

WIA_DPS_PAGE_SIZE = WIA_PAGE_LETTER WIA_DPS_PAGE_HEIGHT = 11000 WIA_DPS_PAGE_WIDTH = 8500 WIA_IPS_ORIENTATION = LANSCAPE WIA_IPS_XPOS = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 1100 WIA_IPS_YEXTENT = 850 WIA_IPS_XRES = 100 WIA_IPS_YRES = 100

**示例4：应用程序将 WIA \_ IPS \_ XEXTENT 属性更改为较小的值**

在下面的代码示例中，应用程序将 WIA \_ IPS \_ XEXTENT 属性更改为1000。 微型驱动程序应假设 WIA IPS XEXTENT 的新值 \_ \_ 对于 "wia \_ dps \_ 页面大小" 属性不再有效 \_ ，因此应将 "wia \_ dps 页面大小" 更改为 " \_ \_ wia \_ 页面 \_ 自定义"。 微型驱动程序还必须调整 [**WIA \_ DPS \_ 页面 \_ 宽度**](wia-dps-page-width.md)。

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
<td><p>适用于 Microsoft Windows XP。 对于 Windows Vista 和更高版本，请使用相同的 WIA_IPS_PAGE_SIZE 属性。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**IWiaMiniDrv：:d rvValidateItemProperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)

[**WIA \_ DPS \_ 页面 \_ 高度**](wia-dps-page-height.md)

[**WIA \_ DPS \_ 页面 \_ 大小**](wia-dps-page-size.md)

[**WIA \_ DPS \_ 页面 \_ 宽度**](wia-dps-page-width.md)

[**WIA \_ IP \_ 方向**](wia-ips-orientation.md)

[**WIA \_ IP \_ 页面 \_ 大小**](wia-ips-page-size.md)

[**WIA \_ IP \_ XEXTENT**](wia-ips-xextent.md)

[**WIA \_ IP \_ XPOS**](wia-ips-xpos.md)

[**WIA \_ IP \_ YEXTENT**](wia-ips-yextent.md)

[**WIA \_ IP \_ YPOS**](wia-ips-ypos.md)