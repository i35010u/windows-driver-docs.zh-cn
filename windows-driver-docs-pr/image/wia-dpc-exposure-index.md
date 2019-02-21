---
title: WIA\_DPC\_EXPOSURE\_INDEX
description: WIA\_DPC\_暴露\_索引属性，可以模拟数字摄像机上的电影胶片速度设置。
ms.assetid: 805efbf0-b81f-49fd-82be-536d471d255e
keywords:
- WIA_DPC_EXPOSURE_INDEX 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_EXPOSURE_INDEX
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c62e9f1a6c8663cc9b9a6e06df370825e48a4dbb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541340"
---
# <a name="wiadpcexposureindex"></a>WIA\_DPC\_EXPOSURE\_INDEX


WIA\_DPC\_暴露\_索引属性，可以模拟数字摄像机上的电影胶片速度设置。

## <span id="ddk_wia_dpc_exposure_index_si"></span><span id="DDK_WIA_DPC_EXPOSURE_INDEX_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表或 WIA\_PROP\_范围

访问权限：读取/写入

<a name="remarks"></a>备注
-------

电影速度设置对应于 ISO 标志 (ASA/DIN)。 通常情况下，设备支持离散的枚举的值，但可以通过一系列值实现持续控制。 值为 0xFFFF 的 WIA\_DPC\_暴露\_索引属性对应于自动 ISO 设置。

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
<td><p>在 Windows Vista 和更高版本操作系统中已过时，并应不再使用。 但是，此属性仍定义 Windows Vista 中与应用程序和用于 Windows Server 2003、 Windows XP 和早期版本的 Windows 设备的兼容性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





