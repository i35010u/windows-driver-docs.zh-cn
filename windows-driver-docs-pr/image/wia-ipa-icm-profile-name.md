---
title: WIA \_ IPA \_ ICM \_ 配置文件 \_ 名称
description: WIA \_ IPA \_ ICM \_ PROFILE \_ name 属性包含图像颜色管理 (要求正确解码映像所需的 ICM) 配置文件名称。
keywords:
- WIA_IPA_ICM_PROFILE_NAME 图像设备
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
ms.openlocfilehash: b8e23db0db52ea38e00ddbe8002bd9d588c8cfb6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817297"
---
# <a name="wia_ipa_icm_profile_name"></a>WIA \_ IPA \_ ICM \_ 配置文件 \_ 名称


WIA \_ IPA \_ ICM \_ PROFILE \_ name 属性包含图像颜色管理 (要求正确解码映像所需的 ICM) 配置文件名称。

## <span id="ddk_wia_ipa_icm_profile_name_si"></span><span id="DDK_WIA_IPA_ICM_PROFILE_NAME_SI"></span>


属性类型： VT \_ BSTR

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

应用程序读取 WIA \_ IPA \_ ICM \_ profile \_ NAME 属性，以确定处理映像时要使用的 ICM 配置文件。 WIA 服务基于驱动程序安装文件中的 ICMProfiles 项创建和维护此属性。

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

 

 





