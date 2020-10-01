---
title: DXGKMDT \_ OPM \_ 连接器 \_ 类型枚举
description: 了解 DXGKMDT \_ OPM \_ 连接器 \_ 类型枚举，该枚举是保留供系统使用的。 请勿在您的驱动程序中使用。
ms.assetid: 57A2F351-99F1-425A-99E3-1167CEFF9FDD
keywords:
- DXGKMDT_OPM_CONNECTOR_TYPE 枚举显示设备
topic_type:
- apiref
api_name:
- DXGKMDT_OPM_CONNECTOR_TYPE
api_location:
- D3dkmdt.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9f3ca4c921f5269f7d70d9639cb834e483302223
ms.sourcegitcommit: fc94eb0d5a41ef81c1b3ab91ad725386db0be0c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603657"
---
# <a name="dxgkmdt_opm_connector_type-enumeration"></a>DXGKMDT \_ OPM \_ 连接器 \_ 类型枚举


预留给系统使用。 请勿在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef enum _DXGKMDT_OPM_CONNECTOR_TYPE {
  DXGKMDT_OPM_CONNECTOR_TYPE_OTHER                     = -1,
  DXGKMDT_OPM_CONNECTOR_TYPE_HD15                      = 0,
  DXGKMDT_OPM_CONNECTOR_TYPE_SVIDEO                    = 1,
  DXGKMDT_OPM_CONNECTOR_TYPE_COMPOSITE_VIDEO           = 2,
  DXGKMDT_OPM_CONNECTOR_TYPE_COMPONENT_VIDEO           = 3,
  DXGKMDT_OPM_CONNECTOR_TYPE_DVI                       = 4,
  DXGKMDT_OPM_CONNECTOR_TYPE_HDMI                      = 5,
  DXGKMDT_OPM_CONNECTOR_TYPE_LVDS                      = 6,
  DXGKMDT_OPM_CONNECTOR_TYPE_D_JPN                     = 8,
  DXGKMDT_OPM_CONNECTOR_TYPE_SDI                       = 9,
  DXGKMDT_OPM_CONNECTOR_TYPE_DISPLAYPORT_EXTERNAL      = 10,
  DXGKMDT_OPM_CONNECTOR_TYPE_DISPLAYPORT_EMBEDDED      = 11,
  DXGKMDT_OPM_CONNECTOR_TYPE_UDI_EXTERNAL              = 12,
  DXGKMDT_OPM_CONNECTOR_TYPE_UDI_EMBEDDED              = 13,
  DXGKMDT_OPM_CONNECTOR_TYPE_RESERVED                  = 14,
  DXGKMDT_OPM_CONNECTOR_TYPE_MIRACAST                  = 15,
  DXGKMDT_OPM_COPP_COMPATIBLE_CONNECTOR_TYPE_INTERNAL  = 0x80000000
} DXGKMDT_OPM_CONNECTOR_TYPE;
```

<a name="constants"></a>常量
---------

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_OTHER"></span><span id="dxgkmdt_opm_connector_type_other"></span>**DXGKMDT \_ OPM \_ 连接器 \_ \_ 其他类型**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_HD15"></span><span id="dxgkmdt_opm_connector_type_hd15"></span>**DXGKMDT \_ OPM \_ 连接器 \_ TYPE \_ HD15**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_SVIDEO"></span><span id="dxgkmdt_opm_connector_type_svideo"></span>**DXGKMDT \_ OPM \_ 连接器 \_ TYPE \_ SVIDEO**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_COMPOSITE_VIDEO"></span><span id="dxgkmdt_opm_connector_type_composite_video"></span>**DXGKMDT \_ OPM \_ 连接器 \_ 类型 \_ 复合 \_ 视频**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_COMPONENT_VIDEO"></span><span id="dxgkmdt_opm_connector_type_component_video"></span>**DXGKMDT \_ OPM \_ 连接器 \_ 类型 \_ 组件 \_ 视频**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_DVI"></span><span id="dxgkmdt_opm_connector_type_dvi"></span>**DXGKMDT \_ OPM \_ 连接器 \_ 类型 \_ DVI**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_HDMI"></span><span id="dxgkmdt_opm_connector_type_hdmi"></span>**DXGKMDT \_ OPM \_ 连接器 \_ 类型 \_ HDMI**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_LVDS"></span><span id="dxgkmdt_opm_connector_type_lvds"></span>**DXGKMDT \_ OPM \_ 连接器 \_ TYPE \_ LVDS**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_D_JPN"></span><span id="dxgkmdt_opm_connector_type_d_jpn"></span>**DXGKMDT \_ OPM \_ 连接器 \_ 类型 \_ D \_ JPN**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_SDI"></span><span id="dxgkmdt_opm_connector_type_sdi"></span>**DXGKMDT \_ OPM \_ 连接器 \_ 类型 \_ SDI**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_DISPLAYPORT_EXTERNAL"></span><span id="dxgkmdt_opm_connector_type_displayport_external"></span>**DXGKMDT \_ OPM \_ 连接器 \_ TYPE \_ DISPLAYPORT \_ EXTERNAL**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_DISPLAYPORT_EMBEDDED"></span><span id="dxgkmdt_opm_connector_type_displayport_embedded"></span>**DXGKMDT \_ OPM \_ 连接器 \_ TYPE \_ DISPLAYPORT \_ EMBEDDED**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_UDI_EXTERNAL"></span><span id="dxgkmdt_opm_connector_type_udi_external"></span>**DXGKMDT \_ OPM \_ 连接器 \_ TYPE \_ UDI \_ EXTERNAL**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_UDI_EMBEDDED"></span><span id="dxgkmdt_opm_connector_type_udi_embedded"></span>**DXGKMDT \_ OPM \_ 连接器 \_ TYPE \_ UDI \_ EMBEDDED**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_RESERVED"></span><span id="dxgkmdt_opm_connector_type_reserved"></span>**DXGKMDT \_ OPM \_ 连接器 \_ 类型已 \_ 保留**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_MIRACAST"></span><span id="dxgkmdt_opm_connector_type_miracast"></span>**DXGKMDT \_ OPM \_ 连接器 \_ 类型 \_ MIRACAST**

<span id="DXGKMDT_OPM_COPP_COMPATIBLE_CONNECTOR_TYPE_INTERNAL"></span><span id="dxgkmdt_opm_copp_compatible_connector_type_internal"></span>**DXGKMDT \_ OPM \_ COPP \_ 兼容的 \_ 连接器 \_ 类型 \_ 内部**

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">D3dkmdt (包含 D3dkmdt) </td>
</tr>
</tbody>
</table>

 

 





