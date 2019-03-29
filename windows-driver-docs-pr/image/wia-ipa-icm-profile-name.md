---
title: WIA\_IPA\_ICM\_PROFILE\_NAME
description: WIA\_IPA\_ICM\_配置文件\_NAME 属性包含需要进行正确解码图像的图像颜色管理 (ICM) 配置文件名称。
ms.assetid: bf4874d9-1f08-4aec-8ee3-2a6a11d63956
keywords:
- WIA_IPA_ICM_PROFILE_NAME 成像设备
topic_type:
- apiref
api_name:
- WIA_IPA_ICM_PROFILE_NAME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcb3322a59223d95fa1d50e4bf930ecce47b6d64
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566344"
---
# <a name="wiaipaicmprofilename"></a>WIA\_IPA\_ICM\_PROFILE\_NAME


WIA\_IPA\_ICM\_配置文件\_NAME 属性包含需要进行正确解码图像的图像颜色管理 (ICM) 配置文件名称。

## <span id="ddk_wia_ipa_icm_profile_name_si"></span><span id="DDK_WIA_IPA_ICM_PROFILE_NAME_SI"></span>


属性类型：VT\_BSTR

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_IPA\_ICM\_配置文件\_名称属性来确定要处理图像时使用的 ICM 配置文件。 WIA 服务创建和维护基于 ICMProfiles 条目驱动程序安装文件中此属性。

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

 

 





