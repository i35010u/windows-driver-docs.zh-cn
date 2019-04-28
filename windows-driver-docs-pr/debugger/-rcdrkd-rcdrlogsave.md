---
title: rcdrkd.rcdrlogsave
description: Rcdrkd.rcdrlogsave 扩展将保存驱动程序的录制器缓冲区。
ms.assetid: 2A79064C-A899-4351-A8A6-D8DF31CF9A17
keywords:
- rcdrkd.rcdrlogsave Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rcdrkd.rcdrlogsave
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b4bbaee0bf93d852827e71c617e4bb0fc4b28423
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334327"
---
# <a name="rcdrkdrcdrlogsave"></a>!rcdrkd.rcdrlogsave


**！ Rcdrkd.rcdrlogsave**扩展将保存驱动程序的录制器缓冲区。

```dbgcmd
!rcdrkd.rcdrlogsave DriverName [CaptureFilename ]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span> *DriverName*   
驱动程序，不包括.sys 扩展名的名称。

<span id="_______CaptureFileName______"></span><span id="_______capturefilename______"></span><span id="_______CAPTUREFILENAME______"></span> *CaptureFileName*   
要在其中保存录制器缓冲区 （不包括扩展名.etl） 文件的名称。 如果*CaptureFileName*未指定，则记录器缓冲区保存在*DriverName*.etl。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Rcdrkd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[RCDRKD 扩展](rcdrkd-extensions.md)

 

 






