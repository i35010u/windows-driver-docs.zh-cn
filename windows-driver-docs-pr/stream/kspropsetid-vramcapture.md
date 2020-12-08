---
title: KSPROPSETID \_ VramCapture
description: KSPROPSETID \_ VramCapture
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59c7829b555051cf31cbd8c863af3861f8c5a1d4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794155"
---
# <a name="kspropsetid_vramcapture"></a>KSPROPSETID \_ VramCapture


视频流 pin 支持 **KSPROPSETID \_ VramCapture** 属性集。 此集中的所有属性都是 VRAM surface 捕获和传输的必需属性。

如果这些属性不受支持，则捕获默认为基于曲面的捕获，并传输到系统内存。

此集中的属性项由 KSPROPERTY \_ VIDMEM \_ 传输枚举值指定，如标头文件 *Ksmedia* 中所定义。

**KSPROPSETID \_ VramCapture** 属性集包括以下属性：

[**KSPROPERTY \_ 显示 \_ 适配器 \_ GUID**](ksproperty-display-adapter-guid.md)

[**KSPROPERTY \_ 首选 \_ 捕获 \_ 图面**](ksproperty-preferred-capture-surface.md)

[**KSPROPERTY \_ 当前 \_ 捕获 \_ 图面**](ksproperty-current-capture-surface.md)

[**KSPROPERTY \_ 映射 \_ \_ \_ 到 \_ VRAM 地址的捕获句柄 \_**](ksproperty-map-capture-handle-to-vram-address.md)

 

 





