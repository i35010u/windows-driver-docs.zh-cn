---
title: WIA \_ DPC \_ RGB \_ 增益
description: WIA \_ DPC \_ RGB \_ 增益属性包含以 Null 结尾的 Unicode 字符串，分别表示应用于图像数据的红色、绿色和蓝色增益。
keywords:
- WIA_DPC_RGB_GAIN 图像设备
topic_type:
- apiref
api_name:
- WIA_DPC_RGB_GAIN
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae5960c58cd1662ae3d6e784ac9c4d74ea8b5624
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785167"
---
# <a name="wia_dpc_rgb_gain"></a>WIA \_ DPC \_ RGB \_ 增益


WIA \_ DPC \_ RGB \_ 增益属性包含以 Null 结尾的 Unicode 字符串，分别表示应用于图像数据的红色、绿色和蓝色增益。 例如，"4:25:50" 表示4的红色收益、25的绿色增益以及50的蓝色收益。

## <span id="ddk_wia_dpc_rgb_gain_si"></span><span id="DDK_WIA_DPC_RGB_GAIN_SI"></span>


属性类型： VT \_ BSTR

有效值： WIA " \_ \_ 无" 或 "wia" 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

WIA \_ DPC \_ RGB \_ 增益属性按如下方式进行分析： *R*：*G*：*B*。 *R* 代表红色增益， *G* 表示绿色增益， *B* 代表蓝色增益。 例如，对于红色 = 4，绿色 = 2，蓝色 = 3 的 RGB 比率，RGB 字符串可以是 "4:2:3" 或 "2000:1000:1500"。 这些值彼此相关。 您可以使用较大的数字来增加粒度，但如果红色、绿色和蓝色的比率保持不变，颜色将相同。 此属性值的字符串分析器应支持 *R*、 *G* 和 *B* 的 UINT16 整数。

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

 

 





