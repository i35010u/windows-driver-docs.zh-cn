---
title: storagekd.storadapter
description: Storagekd.storadapter 扩展显示有关指定 Storport 适配器的信息。
ms.assetid: E7EBC2F7-676A-4DD9-ADAA-5C240299013C
keywords:
- storagekd.storadapter Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- storagekd.storadapter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f380c29540e5eaa19dd45e4f5c62ad3e233668a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533778"
---
# <a name="storagekdstoradapter"></a>!storagekd.storadapter


**！ Storagekd.storadapter**扩展显示有关指定的 Storport 适配器的信息。

```dbgcmd
!storagekd.storadapter [Address]  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定 Storport 适配器设备对象的地址。 如果*地址*是省略，将显示所有 Storport 适配器的列表。

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

下面是举例 **！ storagekd.storadapter**显示：

**1: kd&gt; ! storagekd.storadapter**

```dbgcmd
# STORPORT adapters:
==================
## Driver                 Object            Extension          State
-----------------------------------------------------------------
\Driver\vhdmp          fffffa800649a050  fffffa800649a1a0   Working
```

**1: kd&gt; ! storagekd.storadapter fffffa800649a050**

```dbgcmd
ADAPTER
   DeviceObj : fffffa800649a050   AdapterExt: fffffa800649a1a0   DriverObj :  fffffa800507fcb0   
DeviceState : Working
   LowerDO fffffa8005f71e10   PhysicalDO fffffa8005f71e10   
   SlowLock Free   RemLock -666   
   SystemPowerState: Working AdapterPowerState D0   Full Duplex
   Bus 0   Slot 0   DMA 0000000000000000   Interrupt 0000000000000000   
   Allocated ResourceList 0000000000000000   
Translated ResourceList 0000000000000000   
   Gateway: Outstanding 0   Lower 256   High 256
   PortConfigInfo fffffa800649a2d0   
   HwInit fffffa80062e8840   HwDeviceExt fffffa8004b84d70   (112 bytes)
   SrbExt 2256 bytes   LUExt 24 bytes
   
Normal Logical Units: 
   Product                 SCSI ID  Object            Extension          Pnd Out Ct State
   ----------------------------------------------------------------------------------------
   Msft       Virtual Di   0  0  1  fffffa800658a060  fffffa800658a1b0    0   0  0  Working

   Zombie Logical Units: 
   Product                 SCSI ID  Object            Extension          Pnd Out Ct State
   --------------------------------------------------------------------------------------
```

 

 





