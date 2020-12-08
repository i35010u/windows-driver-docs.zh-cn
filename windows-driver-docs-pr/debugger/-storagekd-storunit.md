---
title: storagekd.storunit
description: Storagekd. storunit 扩展显示指定的 Storport 逻辑单元的相关信息。
keywords:
- storagekd storunit Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- storagekd.storunit
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dd35e946480d651c5a6f22084a9d71e5c4eedf72
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817005"
---
# <a name="storagekdstorunit"></a>!storagekd.storunit


**！ Storagekd. storunit** 扩展显示指定的 Storport 逻辑单元的相关信息。

```dbgcmd
!storagekd.storunit [Address] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address"></span><span id="_______address"></span><span id="_______ADDRESS"></span>*地址*  
指定 Storport 单元设备对象的地址。 如果省略 *Address* ，则显示所有 Storport 单元的列表。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 8 及更高版本</strong></p></td>
<td align="left"><p>Storagekd.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

下面是 **！ storunit** 显示的示例 storagekd：

**0： kd &gt; ！ storagekd. storunit**

```dbgcmd
# STORPORT Units:
==================
## Product                 SCSI ID  Object            Extension         Pnd Out Ct  State
--------------------------------------------------------------------------------------
Msft       Virtual Di   0  0  1  fffffa800658a060  fffffa800658a1b0    0   0  0  Working
```

**0： kd &gt; ！ storagekd. storunit fffffa800658a060**

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

 

 





