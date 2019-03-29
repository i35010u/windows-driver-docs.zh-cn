---
title: KSCATEGORY_SYNTHESIZER
description: KSCATEGORY_SYNTHESIZER
ms.assetid: 07713c80-adff-4c3d-a9df-2c2865ef78d9
keywords:
- KSCATEGORY_SYNTHESIZER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_SYNTHESIZER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3c182cb446cf0ea2d4517ac3a939b91ea7e7f2df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577444"
---
# <a name="kscategorysynthesizer"></a>KSCATEGORY_SYNTHESIZER


KSCATEGORY_SYNTHESIZER[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)MIDI 数据转换为波形音频示例或模拟输出信号 (KS) 功能类别。

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
<td align="left"><p>KSCATEGORY_SYNTHESIZER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{DFF220F3-F70F-11D0-B917-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 音频适配器设备驱动程序注册 KSCATEGORY_SYNTHESIZER 向操作系统指示设备支持 KSCATEGORY_SYNTHESIZER 功能分类的实例。

有关如何在一个 INF 文件中注册此功能的类别的示例，请参阅*Ddksynth.inf*软件合成器示例中包含的 INF 文件*src\\音频\\ddksynth* WDK 的目录。

合成器的常规信息，请参阅[MIDI 和 DirectMusic 筛选器](https://msdn.microsoft.com/library/windows/hardware/ff537520)。

有关设备的音频的适配器的接口类的常规信息，请参阅[音频适配器安装设备接口](https://msdn.microsoft.com/library/windows/hardware/ff536813)。

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

 

 





