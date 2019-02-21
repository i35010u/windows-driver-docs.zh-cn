---
title: minipkd.adapters
description: Minipkd.adapters 扩展显示的所有使用 SCSI 端口驱动程序已在系统中，标识的适配器，并与每个适配器关联的单个设备。
ms.assetid: 8571b9ec-1ec9-4adb-8a65-5306e45c3aa6
keywords:
- minipkd.adapters Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.adapters
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b87b3883bf345ce8b394b75fa7ba7d5cb26724e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541831"
---
# <a name="minipkdadapters"></a>!minipkd.adapters


**！ Minipkd.adapters**扩展显示的所有使用 SCSI 端口驱动程序已在系统中，标识的适配器，并与每个适配器关联的单个设备。

```dbgcmd
!minipkd.adapters 
```

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Minipkd.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[SCSI 微型端口调试](scsi-miniport-debugging.md)。

<a name="remarks"></a>备注
-------

显示内容包括驱动程序名称、 设备对象地址，并为每个适配器的设备扩展地址。 为每个适配器显示内容还包括在适配器上每个设备的列表。 对于每个设备显示内容包括设备扩展地址、 SCSI 地址、 设备对象地址和设备的某些标志。 此外，还包含有关插状态和电源状态信息。

下表中显示的标记进行了说明：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>c</p></td>
<td align="left"><p>声明。 指示设备对其具有一个驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>m</p></td>
<td align="left"><p>缺少。 指示设备已存在总线上以前的扫描过程中，但不是在最近一次扫描期间存在的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>E</p></td>
<td align="left"><p>枚举。 指示设备已被报告给插管理器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>v</p></td>
<td align="left"><p>可见。 指示系统已枚举设备。 如果不存在的设备，此标志是更重要。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>p</p></td>
<td align="left"><p>分页。 指示设备处于分页路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p>d</p></td>
<td align="left"><p>转储。 指示设备处于崩溃转储路径，并将用于故障转储。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>h</p></td>
<td align="left"><p>休眠状态。 指示设备处于休眠状态。</p></td>
</tr>
</tbody>
</table>

 

下面是举例 **！ minipkd.adapters**显示：

```dbgcmd
0: kd> !minipkd.adapters
Adapter \Driver\lp6nds35     DO 86334a70         DevExt 86334b28
Adapter \Driver\adpu160m     DO 8633da70         DevExt 8633db28
 LUN 862e60f8 @(0,0,0) c ev     pnp(00/ff) pow(0,0) DevObj 862e6040
 LUN 863530f8 @(0,1,0) c ev p d pnp(00/ff) pow(0,0) DevObj 86353040
 LUN 862e50f8 @(0,2,0) c ev     pnp(00/ff) pow(0,0) DevObj 862e5040
 LUN 863520f8 @(0,6,0)   ev     pnp(00/ff) pow(0,0) DevObj 86352040
Adapter \Driver\adpu160m     DO 86376040         DevExt 863760f8
```

类似于以下错误消息指示的符号路径不正确，并且不指向 Scsiport.sys 符号的正确版本或 Windows 不具有标识使用 SCSI 端口驱动程序的任何适配器。

```dbgcmd
minipkd error (0) <path> ... \minipkd\minipkd.c @ line 435
```

如果[ **！ minipkd.help** ](-minipkd-help.md)扩展命令返回的帮助信息已成功，SCSI 端口符号是否正确。

 

 





