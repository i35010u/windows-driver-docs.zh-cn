---
title: WIA\_DPC\_压缩\_设置
description: WIA\_DPC\_压缩\_设置属性中包含一个范围或一个整数来表示感知到的图像质量列表。
ms.assetid: dfe22ff2-f613-49a5-8c55-38ba851e7ebd
keywords:
- WIA_DPC_COMPRESSION_SETTING 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_COMPRESSION_SETTING
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22a065d99a0c19f47d8a516a6f636a88a073cb4c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567838"
---
# <a name="wiadpccompressionsetting"></a>WIA\_DPC\_压缩\_设置


WIA\_DPC\_压缩\_设置属性中包含一个范围或一个整数来表示感知到的图像质量列表。

## <span id="ddk_wia_dpc_compression_setting_si"></span><span id="DDK_WIA_DPC_COMPRESSION_SETTING_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表或 WIA\_PROP\_范围

访问权限：读取/写入

<a name="remarks"></a>备注
-------

WIA\_DPC\_压缩\_设置属性应大约通过范围广泛的场景内容以线性方式描述感知到的图像质量。 较小的整数表示质量越低 （即，最大压缩） 和更大的整数表示质量更高 （即，最小压缩）。 在设备上任何可用的设置都仅与该设备，因此特定于设备。

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
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





