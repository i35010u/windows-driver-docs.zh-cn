---
title: WIA\_IP\_方向
description: WIA\_IP\_ORIENTATION 属性描述要扫描的文档的当前方向。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: e963d0d1-020c-4ec1-8b67-a89b1fd3e545
keywords:
- WIA_IPS_ORIENTATION 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_ORIENTATION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fe506dc00a0b8c0ef8d50021fa11d2e78ca1959
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348242"
---
# <a name="wiaipsorientation"></a>WIA\_IP\_方向


WIA\_IP\_ORIENTATION 属性描述要扫描的文档的当前方向。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ips_orientation_si"></span><span id="DDK_WIA_IPS_ORIENTATION_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

应用程序设置 WIA\_IP\_ORIENTATION 属性定义的页或映像以获取原始的方向。 详细了解如何使用 WIA\_IPS\_方向，请参阅[ **WIA\_DPS\_页\_大小**](wia-dps-page-size.md)。

下表描述了有效使用 WIA 的常量\_IP\_方向。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>LANSCAPE</p></td>
<td><p>方向为纵向方向相对应的 90 度开始沿逆时针方向旋转。</p></td>
</tr>
<tr class="even">
<td><p>纵向</p></td>
<td><p>方向为 0 度。</p></td>
</tr>
<tr class="odd">
<td><p>ROT180</p></td>
<td><p>方向为纵向方向相对应的 180 度开始沿逆时针方向旋转。</p></td>
</tr>
<tr class="even">
<td><p>ROT270</p></td>
<td><p>方向为 270 度开始沿逆时针方向旋转纵向方向相对应。</p></td>
</tr>
</tbody>
</table>

 

WIA\_IP\_ORIENTATION 属性描述要扫描的文档的方向。 此属性会影响当前扫描帧和提供的页面大小。

WIA\_IPS\_ORIENTATIONis 不同于[ **WIA\_IP\_旋转**](wia-ips-rotation.md)属性，它是指应用到图像的旋转*后*其进行扫描。 因此，WIA ROT180 值\_IP\_方向是 WIA ROT180 值不同\_IP\_旋转。 对于 WIA\_IPS\_方向，ROT180 描述要扫描的物理文档、 相对于扫描方向和 WIA 的方向\_IP\_旋转，ROT180 描述要应用的图像的旋转扫描后。

WIA\_IP\_ORIENTATION 属性是 ADF 项必需和可选的所有其他图像获取项。

**请注意**   WIA 服务中的兼容性层不会添加支持 WIA\_IP\_到不支持的属性仅当从 Microsoft Windows XP WIA 设备翻译的 ADF 项的方向在设备的子项目。 应用程序不应期望 ADF 项将始终支持此属性，并应始终检查，如果 WIA\_IP\_方向在运行时支持。

 

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


[**WIA\_DPS\_PAGE\_SIZE**](wia-dps-page-size.md)

[**WIA\_IP\_旋转**](wia-ips-rotation.md)

 

 






