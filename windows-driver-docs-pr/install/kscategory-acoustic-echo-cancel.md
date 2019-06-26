---
title: KSCATEGORY_ACOUSTIC_ECHO_CANCEL
description: KSCATEGORY_ACOUSTIC_ECHO_CANCEL
ms.assetid: 91440365-be16-4d98-aa91-e186b9ab6359
keywords:
- KSCATEGORY_ACOUSTIC_ECHO_CANCEL 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_ACOUSTIC_ECHO_CANCEL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fdd47dc67f9b4300949bbaaf88acd663c00371dd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374983"
---
# <a name="kscategoryacousticechocancel"></a>KSCATEGORY_ACOUSTIC_ECHO_CANCEL


KSCATEGORY_ACOUSTIC_ECHO_CANCEL[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为定义[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)(KS) 执行回声的功能类别。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特性</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>KSCATEGORY_ACOUSTIC_ECHO_CANCEL</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{BF963D80-C559-11D0-8A2B-00A0C9255AC1}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 音频设备的驱动程序注册 KSCATEGORY_ACOUSTIC_ECHO_CANCEL 向操作系统指示设备支持执行回声 KS 功能分类的实例。

有关设备的音频的适配器的接口类的信息，请参阅[音频适配器安装设备接口](https://docs.microsoft.com/windows-hardware/drivers/audio/installing-device-interfaces-for-an-audio-adapter)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

 

 





