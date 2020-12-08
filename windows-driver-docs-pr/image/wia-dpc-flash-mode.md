---
title: WIA \_ DPC \_ 闪光 \_ 模式
description: WIA \_ DPC \_ FLASH \_ 模式属性定义了照相机设备的当前 FLASH 模式设置。 设备驱动程序枚举此属性支持的值，应用程序将写入此属性以设置照相机设备的闪光模式。
keywords:
- WIA_DPC_FLASH_MODE 图像设备
topic_type:
- apiref
api_name:
- WIA_DPC_FLASH_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0224ec986e59aea7eb3dda65ae3c1799d3025ba1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830455"
---
# <a name="wia_dpc_flash_mode"></a>WIA \_ DPC \_ 闪光 \_ 模式


WIA \_ DPC \_ FLASH \_ 模式属性定义了照相机设备的当前 FLASH 模式设置。 设备驱动程序枚举此属性支持的值，应用程序将写入此属性以设置照相机设备的闪光模式。

## <span id="ddk_wia_dpc_flash_mode_si"></span><span id="DDK_WIA_DPC_FLASH_MODE_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了对此属性有效的六个。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>FLASHMODE_AUTO</p></td>
<td><p>照相机设备确定正确的闪存设置。</p></td>
</tr>
<tr class="even">
<td><p>FLASHMODE_EXTERNALSYNC</p></td>
<td><p>照相机设备配置为与外部闪存单元同步。</p></td>
</tr>
<tr class="odd">
<td><p>FLASHMODE_FILL</p></td>
<td><p>照相机设备配置为闪烁，而不考虑当前照明情况。</p></td>
</tr>
<tr class="even">
<td><p>FLASHMODE_OFF</p></td>
<td><p>照相机设备被配置为 <em>不</em> 刷新拍摄的任何图片。</p></td>
</tr>
<tr class="odd">
<td><p>FLASHMODE_REDEYE_AUTO</p></td>
<td><p>照相机设备通过使用红眼降低来确定正确的闪光设置，而不考虑当前照明情况。</p></td>
</tr>
<tr class="even">
<td><p>FLASHMODE_REDEYE_FILL</p></td>
<td><p>照相机设备配置为使用红眼降低和闪光，而不考虑当前照明情况。</p></td>
</tr>
</tbody>
</table>

 

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

 

 





