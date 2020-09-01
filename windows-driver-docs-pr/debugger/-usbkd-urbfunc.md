---
title: usbkd.urbfunc
description: Usbkd. urbfunc 命令显示 URB 函数代码的名称。
ms.assetid: 111DD6CD-D7DB-4772-B6DD-8EA88587FD1F
keywords:
- usbkd urbfunc Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.urbfunc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ddd33bcce854344644375c6e529a47140f23e6e5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216738"
---
# <a name="usbkdurbfunc"></a>!usbkd.urbfunc


**！ Usbkd. urbfunc**命令显示 URB 函数代码的名称。

```dbgcmd
!usbkd.urbfunc FunctionCode
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______FunctionCode______"></span><span id="_______functioncode______"></span><span id="_______FUNCTIONCODE______"></span>*FunctionCode*   
URB 函数代码的十六进制值。 这些代码是在 usb 中定义的。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是 **！ urbfunc**的输出示例。

```dbgcmd
0: kd> !usbkd.urbfunc 0xA

URB_FUNCTION_ISOCH_TRANSFER (0xA)
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

