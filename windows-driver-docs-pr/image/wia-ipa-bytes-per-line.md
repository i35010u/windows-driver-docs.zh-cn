---
title: WIA \_ IPA \_ 字节 \_ / \_ 行
description: WIA \_ IPA \_ BYTES \_ PER \_ LINE 属性包含图像的一个扫描行中的字节数。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPA_BYTES_PER_LINE 图像设备
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
ms.openlocfilehash: b88f61a9d0d68cd530ebae8d84afc722bc73085f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837725"
---
# <a name="wia_ipa_bytes_per_line"></a>WIA \_ IPA \_ 字节 \_ / \_ 行


WIA \_ IPA \_ BYTES \_ PER \_ LINE 属性包含图像的一个扫描行中的字节数。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipa_bytes_per_line_si"></span><span id="DDK_WIA_IPA_BYTES_PER_LINE_SI"></span>


属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

\_ \_ \_ \_ 对于所有启用了传输的项，Windows VISTA 驱动程序的 WIA IPA BYTES PER LINE 属性是可选的。 如果此属性与 [**wia \_ IPA 的 \_ \_ \_ 行数**](wia-ipa-number-of-lines.md) 和 [**wia \_ IPA \_ 像素 \_ \_**](wia-ipa-pixels-per-line.md) 数属性一起实现，则为 windows Server 2003、windows XP 和早期版本的 windows 设计的应用程序可以估计每行的像素数、每个扫描行所需的字节数，以及图像中的扫描行总数。 这些值不准确，因为图像处理筛选器可能会修改这些属性所表示的实际值。

如果 Windows Vista 驱动程序未提供这些属性，WIA 服务中的兼容层将添加这些属性。 当 WIA 服务添加这些属性时，将使用 [**wia \_ IPA \_ DEPTH**](wia-ipa-depth.md)、 [**wia \_ ips \_ XEXTENT**](wia-ips-xextent.md)和 [**wia \_ ip \_ YEXTENT**](wia-ips-yextent.md) 属性来更新这些属性。

Windows Vista 应用程序始终应该分析映像标头数据，以获取有关该映像的更准确信息，然后就可以从这些属性获取该信息。

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


[**WIA \_ IPA \_ 深度**](wia-ipa-depth.md)

[**WIA \_ IPA \_ \_ 行数 \_**](wia-ipa-number-of-lines.md)

[**WIA \_ \_ \_ 每行 IPA 像素 \_**](wia-ipa-pixels-per-line.md)

[**WIA \_ IP \_ XEXTENT**](wia-ips-xextent.md)

[**WIA \_ IP \_ YEXTENT**](wia-ips-yextent.md)

 

 






