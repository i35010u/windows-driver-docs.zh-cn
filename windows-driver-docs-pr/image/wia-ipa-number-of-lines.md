---
title: WIA\_IPA\_数\_OF\_行
description: WIA\_IPA\_数\_OF\_行属性包含的图像 （即，图像，以像素为单位的垂直高度） 中包含的行数。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 80f69a99-7008-40f1-8d12-1b7e4cf063b4
keywords:
- WIA_IPA_NUMBER_OF_LINES 成像设备
topic_type:
- apiref
api_name:
- WIA_IPA_NUMBER_OF_LINES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 211d0a7261a4778ee84dd271ad2a6b06cbc11526
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564696"
---
# <a name="wiaipanumberoflines"></a>WIA\_IPA\_数\_OF\_行


WIA\_IPA\_数\_OF\_行属性包含的图像 （即，图像，以像素为单位的垂直高度） 中包含的行数。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipa_number_of_lines_si"></span><span id="DDK_WIA_IPA_NUMBER_OF_LINES_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

WIA\_IPA\_数\_OF\_行属性是可选的 Windows Vista 驱动程序的所有已启用传输的项。 如果 WIA\_IPA\_数\_OF\_线条[ **WIA\_IPA\_字节\_每\_行**](wia-ipa-bytes-per-line.md)，并[ **WIA\_IPA\_像素\_每\_行**](wia-ipa-pixels-per-line.md)实现的对于 Windows Server 2003，编写的应用程序Windows XP 和早期 Windows 版本可以估计每个行中，所需的每个扫描行中，字节数和在图像中的扫描线总数的像素的数。 这些值不准确，因为图像处理筛选器可能会更改实际值的 WIA\_IPA\_数\_OF\_线、 WIA\_IPA\_字节\_每个\_线条和 WIA\_IPA\_像素\_每个\_行表示。

如果 Windows Vista 驱动程序不提供这些属性，WIA 服务中的兼容性层将添加这些属性。 当 WIA 服务将添加这些属性时，它们将更新通过使用[ **WIA\_IPA\_深度**](wia-ipa-depth.md)， [ **WIA\_IP\_大 XEXTENT**](wia-ips-xextent.md)，并[ **WIA\_IP\_YEXTENT** ](wia-ips-yextent.md)属性。

Windows Vista 应用程序应始终会解析映像标头数据，以获取有关可从之前的属性的信息更准确的图像的信息。

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
<td><p>对于 Windows Vista 驱动程序的所有传输启用项可选。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_IPA\_BYTES\_PER\_LINE**](wia-ipa-bytes-per-line.md)

[**WIA\_IPA\_DEPTH**](wia-ipa-depth.md)

[**WIA\_IPA\_PIXELS\_PER\_LINE**](wia-ipa-pixels-per-line.md)

[**WIA\_IPS\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IPS\_YEXTENT**](wia-ips-yextent.md)

 

 






