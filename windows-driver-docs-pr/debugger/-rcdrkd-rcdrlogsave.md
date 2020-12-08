---
title: rcdrkd.rcdrlogsave
description: Rcdrkd. rcdrlogsave 扩展保存驱动程序的记录器缓冲区。
keywords:
- rcdrkd rcdrlogsave Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rcdrkd.rcdrlogsave
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b21de209d0a6a40829fa2b51808dbebe03968e06
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821011"
---
# <a name="rcdrkdrcdrlogsave"></a>!rcdrkd.rcdrlogsave


**！ Rcdrkd rcdrlogsave** 扩展保存驱动程序的记录器缓冲区。

```dbgcmd
!rcdrkd.rcdrlogsave DriverName [CaptureFilename ]
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span>*DriverName*   
驱动程序的名称，不包括 .sys 扩展。

<span id="_______CaptureFileName______"></span><span id="_______capturefilename______"></span><span id="_______CAPTUREFILENAME______"></span>*CaptureFileName*   
文件的名称 (不包括保存记录器缓冲区) 的 .etl 扩展。 如果未指定 *CaptureFileName* ，则记录器缓冲区保存在 *DriverName* 中。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Rcdrkd.dll

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[RCDRKD 扩展](rcdrkd-extensions.md)

 

 






