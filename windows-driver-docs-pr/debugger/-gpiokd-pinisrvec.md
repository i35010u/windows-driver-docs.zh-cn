---
title: gpiokd.pinisrvec
description: Gpiokd. pinisrvec 命令显示 (ISR) 指定 pin 的向量信息的中断服务例程。
keywords:
- gpiokd pinisrvec Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gpiokd.pinisrvec
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9e8ec5a0f5bcf9038bd78da7bcb1771806e908c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824737"
---
# <a name="gpiokdpinisrvec"></a>!gpiokd.pinisrvec


**！ Gpiokd. pinisrvec** 命令显示 (ISR 的中断服务例程) 指定的 pin 的矢量信息。

```dbgcmd
!gpiokd.bankinfo PinAddress
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______PinAddress______"></span><span id="_______pinaddress______"></span><span id="_______PINADDRESS______"></span>*PinAddress*   
表示 pin 的[ \_ GPIO \_ pin \_ 信息 \_ 条目](gpio-extensions.md#data-structures-used-by-the-gpio-commands)数据结构的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Gpiokd.dll

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[GPIO 扩展](gpio-extensions.md)

 

 






