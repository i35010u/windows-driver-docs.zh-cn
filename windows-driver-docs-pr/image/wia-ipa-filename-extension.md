---
title: WIA \_ IPA \_ 文件 \_ 扩展名
description: WIA \_ IPA \_ FILENAME \_ extension 属性包含特定文件格式的文件扩展名。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPA_FILENAME_EXTENSION 图像设备
topic_type:
- apiref
api_name:
- WIA_IPA_FILENAME_EXTENSION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ebf4cc03ca18cc2419d7a0d7bea9d929d838c60
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817315"
---
# <a name="wia_ipa_filename_extension"></a>WIA \_ IPA \_ 文件 \_ 扩展名


WIA \_ IPA \_ FILENAME \_ extension 属性包含特定文件格式的文件扩展名。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipa_filename_extension_si"></span><span id="DDK_WIA_IPA_FILENAME_EXTENSION_SI"></span>


属性类型： VT \_ BSTR

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

微型驱动程序更新了 WIA \_ IPA \_ 文件 \_ 扩展名属性以反映 [**wia \_ IPA \_ FORMAT**](wia-ipa-format.md) 属性的当前值。

例如，如果 WIA \_ IPA \_ 格式为 WiaImgFmt \_ JPEG，wia \_ IPA \_ 文件 \_ 扩展名应为 "jpg"。 如果 WIA \_ IPA \_ 格式为 WiaImgFmt \_ BMP，wia \_ IPA \_ 文件 \_ 扩展名应为 "bmp"。 请注意，文件扩展名不包含句点 ( "。) 。

\_ \_ \_ 对于支持标准格式的驱动程序，建议使用 WIA IPA FILENAME EXTENSION 属性，对于实现自定义格式的驱动程序，建议使用此属性。 WIA \_ IPA \_ FILENAME \_ extension 通知应用程序要在传输私下格式的文件期间使用正确的文件扩展名。 例如，如果 a. Datum Corporation 创建了一个以新格式传输文件的 WIA 驱动程序，则该公司可以指定扩展 "adc"。 此扩展使应用程序可以将该格式的数据传输到文件并创建 *myfile.txt* 之类的文件名，这对了解新扩展的其他人很有用。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ IPA \_ 格式**](wia-ipa-format.md)

 

 






