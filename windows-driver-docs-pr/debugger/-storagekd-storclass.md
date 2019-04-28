---
title: storagekd.storclass
description: Storagekd.storclass 扩展显示有关指定 classpnp 会设备的信息。
ms.assetid: EC5B44F5-540E-4F25-80AA-09BE4F78BF72
keywords:
- storagekd.storclass Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- storagekd.storclass
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a9b6875f23e6430fc05c50a3e89148d590cfb1e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334231"
---
# <a name="storagekdstorclass"></a>!storagekd.storclass


**！ Storagekd.storclass**扩展显示有关指定的信息*classpnp 会*设备。

```dbgcmd
!storagekd.storclass [Address [Level]] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address"></span><span id="_______address"></span><span id="_______ADDRESS"></span> *Address*  
指定的设备对象或 classpnp 会设备的设备扩展到的地址。 如果*地址*是省略，将显示所有 classpnp 会扩展的列表。

<span id="_______Level"></span><span id="_______level"></span><span id="_______LEVEL"></span> *级别*  
指定要显示的详细信息。 此参数可以设置为 0、 1 或 2，2 提供最详尽数据和 0 最少。 默认值为 0。

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

下面是举例 **！ storagekd.storclass**显示：

**1: kd&gt; !storagekd.storclass**

```dbgcmd
Storage class devices:

* !storclass fffffa80043dc060 [1,2] ST3160812AS Paging Disk       
  !storclass fffffa8006581740 [1,2] Msft Virtual Disk Disk       

Usage: !storclass <class device> <level [0-2]>
```

**1: kd&gt; !storagekd.storclass fffffa80043dc060 1**

```dbgcmd
Storage class device fffffa80043dc060 with extension at fffffa80043dc1b0

Classpnp Internal Information at fffffa8003bec360

    Transfer Packet Engine:

     Packet          Status  DL Irp          Opcode  Sector/ListId   UL Irp 
    --------         ------ --------         ------ --------------- --------

    Pending Idle Requests: 0x0


    -- dt classpnp!_CLASS_PRIVATE_FDO_DATA fffffa8003bec360 --

Classpnp External Information at fffffa80043dc1b0

    ST3160812AS 3.ADH             9LS20QRL 

    Minidriver information at fffffa80043dc670
    Attached device object at fffffa800410a060
    Physical device object at fffffa800410a060

    Media Geometry:

        Bytes in a Sector = 512
        Sectors per Track = 63
        Tracks / Cylinder = 255
        Media Length      = 160000000000 bytes = ~149 GB

    -- dt classpnp!_FUNCTIONAL_DEVICE_EXTENSION fffffa80043dc1b0 --
```

 

 





