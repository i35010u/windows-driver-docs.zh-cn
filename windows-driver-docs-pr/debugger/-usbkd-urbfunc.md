---
title: usbkd.urbfunc
description: Usbkd.urbfunc 命令显示 URB 函数代码的名称。
ms.assetid: 111DD6CD-D7DB-4772-B6DD-8EA88587FD1F
keywords:
- usbkd.urbfunc Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.urbfunc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: afbe8a9d5915483a3dbeae3f7ede46815c934dc8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334118"
---
# <a name="usbkdurbfunc"></a>!usbkd.urbfunc


**！ Usbkd.urbfunc**命令显示 URB 函数代码的名称。

```dbgcmd
!usbkd.urbfunc FunctionCode
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______FunctionCode______"></span><span id="_______functioncode______"></span><span id="_______FUNCTIONCODE______"></span> *FunctionCode*   
URB 函数代码的十六进制值。 Usb.h 中定义了这些代码。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是输出的示例 **！ urbfunc**。

```dbgcmd
0: kd> !usbkd.urbfunc 0xA

URB_FUNCTION_ISOCH_TRANSFER (0xA)
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






