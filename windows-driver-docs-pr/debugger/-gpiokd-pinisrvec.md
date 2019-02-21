---
title: gpiokd.pinisrvec
description: Gpiokd.pinisrvec 命令显示指定的 pin 的中断服务例程 (ISR) 向量信息。
ms.assetid: 83D4C072-92B2-4F61-A099-0BA4F8255BE8
keywords:
- gpiokd.pinisrvec Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gpiokd.pinisrvec
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4cf71c9760f57ff8ad90eaa1bc7886419c64330b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554046"
---
# <a name="gpiokdpinisrvec"></a>!gpiokd.pinisrvec


**！ Gpiokd.pinisrvec**命令显示指定的 pin 的中断服务例程 (ISR) 向量信息。

```dbgcmd
!gpiokd.bankinfo PinAddress
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______PinAddress______"></span><span id="_______pinaddress______"></span><span id="_______PINADDRESS______"></span> *PinAddress*   
地址[ \_GPIO\_PIN\_信息\_条目](gpio-extensions.md#data-structures-used-by-the-gpio-commands)数据结构，它表示 pin。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Gpiokd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[GPIO 扩展](gpio-extensions.md)

 

 






