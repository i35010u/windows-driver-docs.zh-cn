---
title: KSCATEGORY_ENCODER
description: KSCATEGORY_ENCODER
keywords:
- KSCATEGORY_ENCODER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_ENCODER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dae892c43c2a099f80815b49adfdc1ece70ec4d4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795487"
---
# <a name="kscategory_encoder"></a>KSCATEGORY_ENCODER


KSCATEGORY_ENCODER [设备接口类](./overview-of-device-interface-classes.md) 是为 [内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义的，用于对数据进行编码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Attribute</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>KSCATEGORY_ENCODER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{19689BF6-C384-48fd-AD51-90E58C79F70B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序将注册 KSCATEGORY_ENCODER 的实例，以向操作系统指示设备支持 KSCATEGORY_ENCODER 功能类别。

有关如何在 INF 文件中注册此功能类别的示例，请参阅 WDK 的 *src/swtuner/algtuner* 目录中的软件调谐器示例附带的 *Bdan* inf 文件。

有关编码器的信息，请参阅 [编码器设备](../stream/encoder-devices.md) 和 [编码器安装和注册](../stream/encoder-installation-and-registration.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows Vista、Windows Server 2003、Windows XP Service Pack 1 (SP1) 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

 

