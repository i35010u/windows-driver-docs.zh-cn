---
title: WIA\_IPS\_LAMP\_AUTO\_OFF
description: WIA\_IPS\_LAMP\_自动\_关闭属性的自动关闭扫描仪的 lamp 包含当前的配置设置。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 82a3b5dc-0a70-4e2a-a863-6019b04cbbaf
keywords:
- WIA_IPS_LAMP_AUTO_OFF 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_LAMP_AUTO_OFF
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d296fb17bee8a6948a39815629aa882801c84666
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348335"
---
# <a name="wiaipslampautooff"></a>WIA\_IPS\_LAMP\_AUTO\_OFF


WIA\_IPS\_LAMP\_自动\_关闭属性的自动关闭扫描仪的 lamp 包含当前的配置设置。 WIA 微型驱动程序创建并维护此属性。

属性类型：VT\_UI4

有效值：WIA\_PROP\_RANGE

访问权限：读取/写入

<a name="remarks"></a>备注
-------

WIA\_IPS\_LAMP\_自动\_关闭属性以编程方式控制的时间长度 lamp 将保留不使用扫描程序时; 此 lamp 可能是专用的 lamp （适用于的透明度适配器） 或主扫描程序 lamp （适用于专用的电影扫描程序）。

应实现 WIA\_IPS\_LAMP\_自动\_关闭仅当设备支持自动 lamp 关闭功能。

有效值为 WIA\_IPS\_LAMP\_自动\_关闭范围从 0 到 4095 秒。

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
<td><p>在 Windows Vista 和更高版本操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





