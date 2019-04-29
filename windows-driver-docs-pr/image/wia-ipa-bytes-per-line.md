---
title: WIA\_IPA\_BYTES\_PER\_LINE
description: WIA\_IPA\_字节\_每\_行属性包含的图像的一个扫描行中的字节数。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: f746ce05-5dfe-47fe-857a-967a6144de16
keywords:
- WIA_IPA_BYTES_PER_LINE 成像设备
topic_type:
- apiref
api_name:
- WIA_IPA_BYTES_PER_LINE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e79195687a1199ec7bffd9336dd651e63127a6e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369559"
---
# <a name="wiaipabytesperline"></a>WIA\_IPA\_BYTES\_PER\_LINE


WIA\_IPA\_字节\_每\_行属性包含的图像的一个扫描行中的字节数。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipa_bytes_per_line_si"></span><span id="DDK_WIA_IPA_BYTES_PER_LINE_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

WIA\_IPA\_字节\_每\_行属性是可选的 Windows Vista 驱动程序的所有已启用传输的项。 如果此属性一起使用[ **WIA\_IPA\_数\_OF\_行**](wia-ipa-number-of-lines.md)并[ **WIA\_IPA\_像素\_每\_行**](wia-ipa-pixels-per-line.md)属性实现，可以估计应用程序设计为 Windows Server 2003、 Windows XP 和早期版本的 Windows每个行、 所需的每个扫描行中，字节数和在图像中的扫描线总数的像素数。 这些值不准确，因为图像处理筛选器可能会更改这些属性表示的实际值。

如果 Windows Vista 驱动程序不提供这些属性，WIA 服务中的兼容性层将添加这些属性。 当 WIA 服务将添加这些属性时，它们将更新通过使用[ **WIA\_IPA\_深度**](wia-ipa-depth.md)， [ **WIA\_IP\_大 XEXTENT**](wia-ips-xextent.md)，并[ **WIA\_IP\_YEXTENT** ](wia-ips-yextent.md)属性。

Windows Vista 应用程序应始终会解析要获取更准确的信息在映像上的映像标头数据，然后可从这些属性。

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
<td><p>对于 Windows Vista 驱动程序的所有传输启用项可选。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_IPA\_DEPTH**](wia-ipa-depth.md)

[**WIA\_IPA\_数\_OF\_行**](wia-ipa-number-of-lines.md)

[**WIA\_IPA\_PIXELS\_PER\_LINE**](wia-ipa-pixels-per-line.md)

[**WIA\_IPS\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IPS\_YEXTENT**](wia-ips-yextent.md)

 

 






