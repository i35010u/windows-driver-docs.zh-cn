---
title: rcdrkd.rcdrloglist
description: Rcdrkd. rcdrloglist 扩展显示驱动程序或一组驱动程序所拥有的记录器日志的列表。
keywords:
- rcdrkd rcdrloglist Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rcdrkd.rcdrloglist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9755f86c000fe7da4bd1bbd0aa6e366659ad30c9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837583"
---
# <a name="rcdrkdrcdrloglist"></a>!rcdrkd.rcdrloglist


**！ Rcdrkd rcdrloglist** 扩展显示驱动程序或一组驱动程序所拥有的记录器日志的列表。

```dbgcmd
!rcdrkd.rcdrloglist DriverName [DriverName ...]
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span>*DriverName*   
驱动程序的名称，不包括 .sys 扩展。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Rcdrkd.dll

<a name="remarks"></a>备注
-------

此命令仅与使用 WppRecorder API 将消息记录到不同日志的驱动程序相关。

<a name="examples"></a>示例
--------

以下示例显示了 USB 3.0 主机控制器驱动程序所拥有的所有记录器日志的列表 ( # A0) 。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[RCDRKD 扩展](rcdrkd-extensions.md)

 

 






