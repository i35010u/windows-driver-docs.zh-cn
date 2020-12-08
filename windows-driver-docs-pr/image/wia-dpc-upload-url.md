---
title: WIA \_ DPC \_ 上传 \_ URL
description: WIA \_ DPC \_ 上传 \_ url 属性描述标准 Internet URL。
keywords:
- WIA_DPC_UPLOAD_URL 图像设备
topic_type:
- apiref
api_name:
- WIA_DPC_UPLOAD_URL
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9dcf81e1382f63d5b12afa9b1b13eb239a178ca8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802413"
---
# <a name="wia_dpc_upload_url"></a>WIA \_ DPC \_ 上传 \_ URL


WIA \_ DPC \_ 上传 \_ url 属性描述标准 Internet URL。

## <span id="ddk_wia_dpc_upload_url_si"></span><span id="DDK_WIA_DPC_UPLOAD_URL_SI"></span>


属性类型： VT \_ BSTR

有效值： WIA " \_ \_ 无"

访问权限：读/写

<a name="remarks"></a>备注
-------

WIA \_ DPC \_ 上传 \_ url 属性介绍了从设备获取图像或对象后，可以将其上传到的 url：

-   WIA 应用程序将读取 WIA \_ DPC \_ 上传 \_ url，并允许用户自动将图像上传到 URL。

-   应用程序设置 URL 和其他设备 (例如，网亭) 使用 WIA \_ DPC \_ 上载 \_ URL。

Microsoft Windows 操作系统不上传图像。

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
<td><p>在 Windows Vista 和更高版本的操作系统中已过时，不应再使用。 但是，在 Windows Vista 中仍定义此属性，以与为 Windows Server 2003、Windows XP 和 windows 的早期版本设计的应用程序和设备兼容。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





