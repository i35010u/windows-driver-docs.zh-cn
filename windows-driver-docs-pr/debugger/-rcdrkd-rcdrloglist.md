---
title: rcdrkd.rcdrloglist
description: Rcdrkd.rcdrloglist 扩展显示驱动程序或驱动程序的一组所拥有的刻录机日志的列表。
ms.assetid: D4D3C313-EFD4-482B-B4A3-307F2407D2BA
keywords:
- rcdrkd.rcdrloglist Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rcdrkd.rcdrloglist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c4de589f5c06e062baa4846a512a688674de7255
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335784"
---
# <a name="rcdrkdrcdrloglist"></a>!rcdrkd.rcdrloglist


**！ Rcdrkd.rcdrloglist**扩展显示的驱动程序或驱动程序的一组所拥有的刻录机日志列表。

```dbgcmd
!rcdrkd.rcdrloglist DriverName [DriverName ...]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span> *DriverName*   
驱动程序，不包括.sys 扩展名的名称。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Rcdrkd.dll

<a name="remarks"></a>备注
-------

此命令将仅适用于使用 WppRecorder API 将消息记录到不同的日志的驱动程序。

<a name="examples"></a>示例
--------

下面的示例显示通过 USB 3.0 主机控制器驱动程序 (usbxhci.sys) 所拥有的所有记录器日志的列表。

```dbgcmd
3: kd> !rcdrloglist usbxhci
Log dump command                           Log ID                   Size
================                           ======                   ====
!rcdrlogdump  usbxhci -a fffffa8005ff2b60  03 SLT02 DCI04           1024
!rcdrlogdump  usbxhci -a fffffa8005ff2010  03 SLT02 DCI03           1024
!rcdrlogdump  usbxhci -a fffffa8005b36010  03 SLT01 DCI03           1024
!rcdrlogdump  usbxhci -a fffffa8005b379e0  03 SLT01 DCI04           1024
!rcdrlogdump  usbxhci -a fffffa8005b33350  03 SLT02 DCI01           1024
!rcdrlogdump  usbxhci -a fffffa8005b2bb60  03 SLT01 DCI01           1024
!rcdrlogdump  usbxhci -a fffffa8005a2bb60  03 CMD                   1024
!rcdrlogdump  usbxhci -a fffffa8005a1ab60  03 INT00                 1024
!rcdrlogdump  usbxhci -a fffffa8005085330  03 RUNDOWN               512
!rcdrlogdump  usbxhci -a fffffa8005311780  03 1033 0194             1024
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[RCDRKD 扩展](rcdrkd-extensions.md)

 

 






