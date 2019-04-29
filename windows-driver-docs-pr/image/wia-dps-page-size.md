---
title: WIA\_DPS\_PAGE\_SIZE
description: WIA\_DPS\_页\_SIZE 属性包含当前选定要扫描的页的大小。
ms.assetid: 16e32b83-26b8-4283-a937-9fbbe77b42b8
keywords:
- WIA_DPS_PAGE_SIZE 成像设备
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
ms.openlocfilehash: fa377ae400a9a5da4a0ba92fe68c4eb649f6848a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380943"
---
# <a name="wiadpspagesize"></a>WIA\_DPS\_PAGE\_SIZE


WIA\_DPS\_页\_SIZE 属性包含当前选定要扫描的页的大小。

## <span id="ddk_wia_dps_page_size_si"></span><span id="DDK_WIA_DPS_PAGE_SIZE_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

若要选择要扫描的页的尺寸，应用程序在设置 WIA\_DPS\_页\_大小。 WIA 微型驱动程序创建并维护此属性。

下表描述了与有效的常量[ **WIA\_IPS\_页\_大小**](wia-ips-page-size.md)。

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
<td><p>页大小为 8267 × 11692 （纵向）。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PAGE_CUSTOM</p></td>
<td><p>值定义的页面大小<a href="wia-dps-page-height.md" data-raw-source="[&lt;strong&gt;WIA_DPS_PAGE_HEIGHT&lt;/strong&gt;](wia-dps-page-height.md)"> <strong>WIA_DPS_PAGE_HEIGHT</strong> </a>并<a href="wia-dps-page-width.md" data-raw-source="[&lt;strong&gt;WIA_DPS_PAGE_WIDTH&lt;/strong&gt;](wia-dps-page-width.md)"> <strong>WIA_DPS_PAGE_WIDTH</strong> </a>属性。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PAGE_LETTER</p></td>
<td><p>页大小为 8500 × 11000 （纵向）。</p></td>
</tr>
</tbody>
</table>

 

值[ **WIA\_IPS\_方向**](wia-ips-orientation.md)属性确定当前所选页面的方向。 WIA\_DPS\_页面\_宽度和 WIA\_DPS\_页\_高度属性报告页面的尺寸，以英寸为单位的千分之几秒 (。 001)。 这些属性必须具有值等效于[ **WIA\_IPS\_大 XEXTENT** ](wia-ips-xextent.md)并[ **WIA\_IP\_YEXTENT** ](wia-ips-yextent.md)属性，其中包含页面的尺寸，以像素为单位。

WIA\_PROP\_列表类型化的值应依赖于有效的设置的 WIA\_IP\_ORIENTATION 属性。 如果设备无法扫描具有 WIA 横向的文档\_页上\_A4 设置，WIA\_页面\_A4 不应出现在列表中的有效值为 WIA\_DPS\_页\_SIZE 属性时 WIA\_IP\_方向将设置为 LANSCAPE。

如果应用程序设置 WIA\_DPS\_页面\_WIA 以外的任何值的大小\_页\_自定义，微型驱动程序应调整 WIA 的值\_DPS\_页\_宽度和 WIA\_DPS\_页\_到页面的尺寸，在千分之几英寸为单位的高度 (。 001)。 微型驱动程序还应调整 WIA 的值\_IPS\_大 XEXTENT 和 WIA\_IP\_YEXTENT 到页面的尺寸，以像素为单位。

如果扩展盘区设置 (WIA\_IPS\_大 XEXTENT 或 WIA\_IP\_YEXTENT) 更改为值执行*不*与当前的页面大小设置匹配，应更改微型驱动程序值 WIA\_DPS\_页面\_大小属性设置为 WIA\_页\_自定义。 微型驱动程序还应修改 WIA\_DPS\_页面\_宽度或 WIA\_DPS\_页\_根据新的范围设置的高度。

如果 WIA\_IP\_方向将设置为 LANSCAPE、 范围设置将"翻转。" 例如，如果应用程序设置 WIA\_DPS\_页面\_大小不超过 WIA\_页\_A4，微型驱动程序应设置 WIA\_DPS\_页\_11692 的宽度和WIA\_DPS\_页\_8267 的高度。 (微型驱动程序还应设置 WIA\_IPS\_大 XEXTENT 和 WIA\_IP\_YEXTENT 相应。)请注意，如果 WIA\_DPS\_页面\_大小设置为 WIA\_页\_自定义，方向设置不用于确定要扫描的页的区域维度。

微型驱动程序必须确保 WIA\_IP\_ORIENTATION 属性同意与当前所选内容区域。 如果应用程序更改的值 WIA\_IP\_方向设为一个无效的当前所选的页面大小，微型驱动程序应更改 WIA 的值\_DPS\_页\_到页面大小支持的新的方向值的大小。

如果应用程序设置 WIA\_DPS\_页面\_大小属性设置为 WIA\_页\_自定义的当前选择区域不受影响。 WIA 微型驱动程序应获取当前的图像布局中，从当前的设置开始[ **WIA\_IPS\_XPOS** ](wia-ips-xpos.md)并[ **WIA\_IPS\_YPOS** ](wia-ips-ypos.md)属性。 如果在外部扫描程序的平台上的所选内容区域中的结果的页面大小设置，微型驱动程序必须自动调整 WIA 的值\_IPS\_XPOS 和 WIA\_IP\_YPOS 属性设置为有效设置。 如果 WIA\_DPS\_页面\_大小和 WIA\_IP\_方向属性设置在同一时间并且它们是无效的它们应用结合使用时，微型驱动程序应失败通过返回中的错误的应用程序的设置[ **IWiaMiniDrv::drvValidateItemProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff545017)方法。

下面的四个代码示例演示以下 WIA\_DPS\_页\_大小方案：

1.  该驱动程序报告的设置。

2.  应用程序设置 WIA\_DPS\_页面\_大小属性设置为 WIA\_页\_字母。

3.  应用程序设置[ **WIA\_IPS\_方向**](wia-ips-orientation.md) LANSCAPE 属性。

4.  应用程序更改[ **WIA\_IPS\_大 XEXTENT** ](wia-ips-xextent.md)属性设置为较小的值。

**示例 1:微型驱动程序报告的设置**

在下面的代码示例中，微型驱动程序之前应用程序设置任何 WIA 属性设置自定义选择区域。 在这种情况下，选择区域表示整个平板。

WIA_DPS_PAGE_SIZE = WIA_PAGE_CUSTOM WIA_DPS_PAGE_WIDTH = 11500 WIA_DPS_PAGE_HEIGHT = 14000 WIA_IPS_ORIENTATION = 纵向 WIA_IPS_XPOS = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 1150 WIA_IPS_YEXTENT = 1400 WIA_IPS_XRES = 100 WIA_IPS_YRES = 100

**示例 2:应用程序设置 WIA\_DPS\_页面\_大小属性设置为 WIA\_页\_字母**

WIA_DPS_PAGE_SIZE = WIA_PAGE_LETTER WIA_DPS_PAGE_WIDTH = 8500 WIA_DPS_PAGE_HEIGHT = 11000 WIA_IPS_ORIENTATION = 纵向 WIA_IPS_XPOS = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 850 WIA_IPS_YEXTENT = 1100 WIA_IPS_XRES = 100 WIA_IPS_YRES = 100

**示例 3:应用程序设置 WIA\_IP\_LANSCAPE 方向属性**

物理平台必须能够获取最初在横向方向的页面。

WIA_DPS_PAGE_SIZE = WIA_PAGE_LETTER WIA_DPS_PAGE_HEIGHT = 11000 WIA_DPS_PAGE_WIDTH = 8500 WIA_IPS_ORIENTATION = LANSCAPE WIA_IPS_XPOS = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 1100 WIA_IPS_YEXTENT = 850 WIA_IPS_XRES = 100 WIA_IPS_YRES = 100

**示例 4:应用程序更改 WIA\_IP\_大 XEXTENT 属性设置为较小的值**

在下面的代码示例中，应用程序更改 WIA\_IP\_大 XEXTENT 属性设置为 1000年。 微型驱动程序应假定 WIA 的新值\_IPS\_大 XEXTENT 不再有效的 WIA\_DPS\_页\_SIZE 属性，从而应更改 WIA\_DPS\_页面\_WIA 的大小\_页\_自定义。 微型驱动程序还必须调整[ **WIA\_DPS\_页\_宽度**](wia-dps-page-width.md)。

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
<td><p>Version</p></td>
<td><p>适用于 Microsoft Windows XP。 适用于 Windows Vista 及更高版本，使用相同的 WIA_IPS_PAGE_SIZE 属性。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**IWiaMiniDrv::drvValidateItemProperties**](https://msdn.microsoft.com/library/windows/hardware/ff545017)

[**WIA\_DPS\_PAGE\_HEIGHT**](wia-dps-page-height.md)

[**WIA\_DPS\_PAGE\_SIZE**](wia-dps-page-size.md)

[**WIA\_DPS\_PAGE\_WIDTH**](wia-dps-page-width.md)

[**WIA\_IP\_方向**](wia-ips-orientation.md)

[**WIA\_IPS\_PAGE\_SIZE**](wia-ips-page-size.md)

[**WIA\_IPS\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IPS\_XPOS**](wia-ips-xpos.md)

[**WIA\_IPS\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IPS\_YPOS**](wia-ips-ypos.md)
