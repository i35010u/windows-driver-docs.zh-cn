---
title: bthkd.bthusbtransfer
description: Bthkd. bthusbtransfer 命令显示蓝牙 usb 传输上下文，包括 Irp、Bip 和传输缓冲区信息。
keywords:
- bthkd bthusbtransfer Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bthkd.bthusbtransfer
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 96905c4846daaaf05f6dcb67e54a9b9115eee0d7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799911"
---
# <a name="bthkdbthusbtransfer"></a>!bthkd.bthusbtransfer


**！ Bthkd. bthusbtransfer** 命令显示蓝牙 usb 传输上下文，包括 Irp、Bip 和传输缓冲区信息。

```dbgsyntax
!bthkd.bthusbtransfer addr 
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______addr______"></span><span id="_______ADDR______"></span>*地址*   
蓝牙 USB 传输上下文的地址。

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


可以使用！ bthinfo 命令显示 USB 传输上下文的地址。 它在 "传输列表" 部分下列出。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Bthkd.dll

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[蓝牙扩展 (Bthkd.dll)](bluetooh-extensions--bthkd-dll-.md)

 

 






