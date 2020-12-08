---
title: minipkd 适配器
description: Minipkd 扩展显示与系统中已标识的 SCSI 端口驱动程序以及与每个适配器关联的各个设备一起使用的所有适配器。
keywords:
- minipkd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.adapters
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1827167adb5f4788c04668794dec0a5f6114a8e2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798435"
---
# <a name="minipkdadapters"></a>!minipkd.adapters


**！ Minipkd** extension 显示了所有与系统中已标识的 SCSI 端口驱动程序配合使用的适配器，以及与每个适配器关联的单独设备。

```dbgcmd
!minipkd.adapters 
```

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [SCSI 微型端口调试](scsi-miniport-debugging.md)。

<a name="remarks"></a>备注
-------

显示内容包括每个适配器的驱动程序名称、设备对象地址以及设备扩展地址。 每个适配器的显示还包括适配器上每个设备的列表。 每个设备的显示内容包括设备扩展地址、SCSI 地址、设备对象地址以及设备的某些标志。 还包括有关即插即用状态和电源状态的信息。

下表说明了显示中的标志：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">标志</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>c</p></td>
<td align="left"><p>声明. 指示设备上有一个驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>m</p></td>
<td align="left"><p>缺失值。 指示设备在以前的扫描中出现在总线上，但在最新扫描期间不存在。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>E</p></td>
<td align="left"><p>列举. 指示已将设备报告给即插即用管理器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>v</p></td>
<td align="left"><p>亮起. 指示设备已由系统枚举。 如果设备不存在此标志，则此标志更有效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>p</p></td>
<td align="left"><p>分页. 指示设备在分页路径中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>d</p></td>
<td align="left"><p>转储. 指示设备处于崩溃转储路径，并且将用于故障转储。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>h</p></td>
<td align="left"><p>R. 指示设备处于休眠状态。</p></td>
</tr>
</tbody>
</table>

 

下面是 **！ minipkd** 显示的示例：

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

类似于以下内容的错误消息指示符号路径不正确，并且未指向正确版本的 Scsiport.sys 符号，或者 Windows 尚未识别使用 SCSI 端口驱动程序的任何适配器。

```dbgcmd
minipkd error (0) <path> ... \minipkd\minipkd.c @ line 435
```

如果 [**！ minipkd**](-minipkd-help.md) extension 命令成功返回帮助信息，则 SCSI 端口符号正确。

 

 





