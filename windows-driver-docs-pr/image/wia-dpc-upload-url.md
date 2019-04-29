---
title: WIA\_DPC\_上传\_URL
description: WIA\_DPC\_上传\_URL 属性描述标准的 Internet URL。
ms.assetid: 5fc36640-32e3-4e51-845f-dabaecd39472
keywords:
- WIA_DPC_UPLOAD_URL 成像设备
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
ms.openlocfilehash: 64803dd2ad6fbb3e113fde4c2f852b1f7449aefd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391709"
---
# <a name="wiadpcuploadurl"></a>WIA\_DPC\_上传\_URL


WIA\_DPC\_上传\_URL 属性描述标准的 Internet URL。

## <span id="ddk_wia_dpc_upload_url_si"></span><span id="DDK_WIA_DPC_UPLOAD_URL_SI"></span>


属性类型：VT\_BSTR

有效值：WIA\_PROP\_NONE

访问权限：读取/写入

<a name="remarks"></a>备注
-------

WIA\_DPC\_上传\_URL 属性描述图像或对象后从一台设备，获得, 可上载到以下方案之一中的 URL:

-   WIA 应用程序读取 WIA\_DPC\_上传\_URL，并允许用户以自动将图像上载到的 URL。

-   应用程序设置的 URL，而其他设备 （例如，网亭） 使用 WIA\_DPC\_上传\_URL。

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
<td><p>Version</p></td>
<td><p>在 Windows Vista 和更高版本操作系统中已过时，并应不再使用。 但是，此属性仍定义 Windows Vista 中与应用程序和用于 Windows Server 2003、 Windows XP 和早期版本的 Windows 设备的兼容性。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





