---
title: WIA \_ IPA \_ \_ 行数 \_
description: WIA \_ IPA \_ number \_ \_ 属性包含图像中包含的行数 (即图像的垂直高度（以像素为单位）) 。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPA_NUMBER_OF_LINES 图像设备
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
ms.openlocfilehash: 953a4833821dfc403c46e32a2c3ecd188c5bb893
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817259"
---
# <a name="wia_ipa_number_of_lines"></a>WIA \_ IPA \_ \_ 行数 \_


WIA \_ IPA \_ number \_ \_ 属性包含图像中包含的行数 (即图像的垂直高度（以像素为单位）) 。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipa_number_of_lines_si"></span><span id="DDK_WIA_IPA_NUMBER_OF_LINES_SI"></span>


属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

\_ \_ \_ \_ 对于所有启用了传输的项，Windows Vista 驱动程序的 "WIA IPA 数目" 属性是可选的。 如果 WIA \_ IPA \_ \_ 的 \_ 行数、 [**\_ \_ \_ 每 \_ 行 wia IPA 字节**](wia-ipa-bytes-per-line.md)数以及 [**\_ \_ \_ 每 \_ 行 wia IPA 像素**](wia-ipa-pixels-per-line.md) ，则为 windows Server 2003、windows XP 和早期版本的 windows 版本编写的应用程序可以估计每行的像素数、每个扫描行所需的字节数，以及图像中的扫描行总数。 这些值是不准确的，因为图像处理筛选器可以修改实际值、WIA \_ IPA \_ \_ 的 \_ 行数、 \_ 每行的 wia IPA 字节数 \_ \_ \_ ， \_ 以及 \_ 每行 wia IPA 像素 \_ \_ 表示。

如果 Windows Vista 驱动程序未提供这些属性，则 WIA 服务中的兼容性层将添加这些属性。 当 WIA 服务添加这些属性时，将使用 [**wia \_ IPA \_ DEPTH**](wia-ipa-depth.md)、 [**wia \_ ips \_ XEXTENT**](wia-ips-xextent.md)和 [**wia \_ ip \_ YEXTENT**](wia-ips-yextent.md) 属性来更新这些属性。

Windows Vista 应用程序应始终分析映像标头数据，以获取与之前属性中提供的信息更精确的映像的相关信息。

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
<td><p>对于所有启用了传输的项，Windows Vista 驱动程序都可选。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ IPA \_ 字节 \_ / \_ 行**](wia-ipa-bytes-per-line.md)

[**WIA \_ IPA \_ 深度**](wia-ipa-depth.md)

[**WIA \_ \_ \_ 每行 IPA 像素 \_**](wia-ipa-pixels-per-line.md)

[**WIA \_ IP \_ XEXTENT**](wia-ips-xextent.md)

[**WIA \_ IP \_ YEXTENT**](wia-ips-yextent.md)

 

 






