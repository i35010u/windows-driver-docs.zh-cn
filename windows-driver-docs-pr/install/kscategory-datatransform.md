---
title: KSCATEGORY_DATATRANSFORM
description: KSCATEGORY_DATATRANSFORM
keywords:
- KSCATEGORY_DATATRANSFORM 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_DATATRANSFORM
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d86f48a574ef3635bcb3b58dca0138871e84072f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829877"
---
# <a name="kscategory_datatransform"></a>KSCATEGORY_DATATRANSFORM


为转换音频数据流的[内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义 KSCATEGORY_DATATRANSFORM[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>KSCATEGORY_DATATRANSFORM</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{2EB07EA0-7E70-11D0-A5D6-28DB04C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序将注册 KSCATEGORY_DATATRANSFORM 的实例，以向操作系统指示设备支持 KSCATEGORY_DATATRANSFORM 功能类别。

有关如何在 INF 文件中注册此功能类别的示例，请参阅 WDK 的 *src \\ 音频 \\ Ddksynth* 目录中的软件合成器示例附带的 *Ddksynth* inf 文件。

有关此功能类别的详细信息，请参阅 [安装音频适配器的设备接口](../audio/installing-device-interfaces-for-an-audio-adapter.md)、 [**KSPROPERTY_TOPOLOGY_CATEGORIES**](../stream/ksproperty-topology-categories.md)以及 [GFX 筛选器工厂的要求](../audio/index.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

 

