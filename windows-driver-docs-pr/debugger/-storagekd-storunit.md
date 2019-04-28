---
title: storagekd.storunit
description: Storagekd.storunit 扩展显示有关指定 Storport 逻辑单元的信息。
ms.assetid: 73A2632C-962E-4075-97B9-5D7D843E9D0F
keywords:
- storagekd.storunit Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- storagekd.storunit
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3cc7d844b0cae7c1ebaa2dc2cd3c1c6280722495
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338779"
---
# <a name="storagekdstorunit"></a>!storagekd.storunit


**！ Storagekd.storunit**扩展显示有关指定 Storport 逻辑单元的信息。

```dbgcmd
!storagekd.storunit [Address] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address"></span><span id="_______address"></span><span id="_______ADDRESS"></span> *Address*  
指定 Storport 单位设备对象的地址。 如果*地址*是省略，此时会显示所有 Storport 单元的列表。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 8 及更高版本</strong></p></td>
<td align="left"><p>Storagekd.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

下面是举例 **！ storagekd.storunit**显示：

**0: kd&gt; !storagekd.storunit**

```dbgcmd
# STORPORT Units:
==================
## Product                 SCSI ID  Object            Extension         Pnd Out Ct  State
--------------------------------------------------------------------------------------
Msft       Virtual Di   0  0  1  fffffa800658a060  fffffa800658a1b0    0   0  0  Working
```

**0: kd&gt; !storagekd.storunit fffffa800658a060**

```dbgcmd
   DO fffffa800658a060   Ext fffffa800658a1b0   Adapter fffffa800649a1a0   Working
   Vendor: Msft       Product: Virtual Disk       SCSI ID: (0, 0, 1)   
   Claimed Enumerated 
   SlowLock Free   RemLock 1   PageCount 0
   QueueTagList: fffffa800658a270      Outstanding: Head fffffa800658a398  Tail fffffa800658a398  Timeout -1
   DeviceQueue fffffa800658a2a0   Depth: 250   Status: Not Frozen   PauseCount: 0   BusyCount: 0   
   IO Gateway: Busy Count 0   Pause Count 0
   Requests: Outstanding 0   Device 0   ByPass 0


[Device-Queued Requests]

## IRP               SRB Type   SRB               XRB               Command           MDL               SGList            Timeout
-----------------------------------------------------------------------------------------------------------------------------------


[Bypass-Queued Requests]

## IRP               SRB Type   SRB               XRB               Command           MDL               SGList            Timeout
-----------------------------------------------------------------------------------------------------------------------------------


[Outstanding Requests]

## IRP               SRB Type   SRB               XRB               Command           MDL               SGList            Timeout
-----------------------------------------------------------------------------------------------------------------------------------


[Completed Requests]

IRP               SRB Type   SRB               XRB               Command           MDL               SGList            Timeout
-----------------------------------------------------------------------------------------------------------------------------------
```

 

 





