---
title: WIA\_IP\_页\_大小
description: WIA\_IPS\_页\_大小属性包含当前选定要扫描的页的大小。
ms.assetid: dcfad67e-31d5-41b8-b471-532626f571af
keywords:
- WIA_IPS_PAGE_SIZE 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PAGE_SIZE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0fc873135dcd03e0e9e83d299cdfe7301720e17
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840683"
---
# <a name="wia_ips_page_size"></a>WIA\_IP\_页\_大小


WIA\_IPS\_页\_大小属性包含当前选定要扫描的页的大小。

属性类型： VT\_I4

有效值： WIA\_的\_列表

访问权限：读/写

<a name="remarks"></a>备注
-------

若要选择要扫描的页的维度，应用程序会将 WIA\_IPS\_页\_大小属性。 WIA 微型驱动程序创建并维护此属性。

下表描述了在 WIA\_IPS\_页\_大小中有效的常量。

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
<td><p>8267×11692（纵向）。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PAGE_AUTO</p></td>
<td><p>用于配置自动页面大小检测。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PAGE_CUSTOM</p></td>
<td><p>由<a href="wia-ips-page-height.md" data-raw-source="[&lt;strong&gt;WIA_IPS_PAGE_HEIGHT&lt;/strong&gt;](wia-ips-page-height.md)"><strong>WIA_IPS_PAGE_HEIGHT</strong></a>和<a href="wia-ips-page-width.md" data-raw-source="[&lt;strong&gt;WIA_IPS_PAGE_WIDTH&lt;/strong&gt;](wia-ips-page-width.md)"><strong>WIA_IPS_PAGE_WIDTH</strong></a>属性的值定义。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PAGE_CUSTOM_BASE</p></td>
<td><p>由 WIA_IPS_PAGE_HEIGHT 和 WIA_IPS_PAGE_WIDTH 属性的值定义。 此值用于定义自定义页面大小，而不是 WIA_PAGE_CUSTOM 值启用的单个页面。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PAGE_LETTER</p></td>
<td><p>8500×11000（纵向）。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p>在 Windows Vista 和更高版本的操作系统中可用。 对于 Windows XP，请改为使用 WIA_DPS_PAGE_SIZE 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef （包括 Wiadef）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**IWiaMiniDrv：:d rvValidateItemProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)

[**WIA\_DPS\_页\_大小**](wia-dps-page-size.md)

[**WIA\_IP\_方向**](wia-ips-orientation.md)

[**WIA\_IP\_页\_高度**](wia-ips-page-height.md)

[**WIA\_IP\_页\_宽度**](wia-ips-page-width.md)

[**WIA\_IP\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IP\_XPOS**](wia-ips-xpos.md)

[**WIA\_IP\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IP\_YPOS**](wia-ips-ypos.md)

 

 






