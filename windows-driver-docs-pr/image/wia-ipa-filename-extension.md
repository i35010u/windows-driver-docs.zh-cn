---
title: WIA\_IPA\_FILENAME\_EXTENSION
description: WIA\_IPA\_文件名\_扩展属性包含特定的文件格式的文件扩展名。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 08abb3f2-73a2-42cd-ae69-1607eda63d1e
keywords:
- WIA_IPA_FILENAME_EXTENSION 成像设备
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
ms.openlocfilehash: 5d83166d781d5b70493106079ecf4d02eaf89b80
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369551"
---
# <a name="wiaipafilenameextension"></a>WIA\_IPA\_FILENAME\_EXTENSION


WIA\_IPA\_文件名\_扩展属性包含特定的文件格式的文件扩展名。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipa_filename_extension_si"></span><span id="DDK_WIA_IPA_FILENAME_EXTENSION_SI"></span>


属性类型：VT\_BSTR

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

微型驱动程序更新 WIA\_IPA\_文件名\_扩展属性以反映的当前值[ **WIA\_IPA\_格式**](wia-ipa-format.md)属性。

例如，如果 WIA\_IPA\_格式是 WiaImgFmt\_JPEG、 WIA\_IPA\_文件名\_扩展名应为"jpg"。 如果 WIA\_IPA\_格式是 WiaImgFmt\_BMP、 WIA\_IPA\_文件名\_扩展名应为"bmp"。 请注意，文件扩展名不包含句点 ("。")。

WIA\_IPA\_文件名\_扩展属性建议的驱动程序，支持标准格式，需对实现自定义格式的驱动程序。 WIA\_IPA\_文件名\_扩展通知正确的文件扩展名的应用程序使用的传输过程中私下格式的文件。 例如，如果 A.Datum Corporation 创建传输新格式的文件中的 WIA 驱动程序，该公司可以指定"adc"的扩展。 此扩展使应用程序将以该格式的数据传输到一个文件，并创建文件名称，如*Myfile.adc*，这很有用的其他人了解新的扩展插件。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_IPA\_格式**](wia-ipa-format.md)

 

 






