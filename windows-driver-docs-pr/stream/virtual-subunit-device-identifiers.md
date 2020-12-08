---
title: 虚拟子单元设备标识符
description: 虚拟子单元设备标识符
keywords:
- AV/C WDK，标识符
- 标识符 WDK AV/C
- 设备 Id WDK AV/C
- Avc.sys 函数驱动程序 WDK，标识符
- 虚拟子单位设备标识符 WDK AV/C
- 子次级支持 WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc1c55c9dc8814ab2dd01637446b96d882669236
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791097"
---
# <a name="virtual-subunit-device-identifiers"></a>虚拟子单元设备标识符


类似于 "设备标识符" (ID 的格式) 字段 "对于 [对等子单元连接](peer-subunit-device-identifiers.md)，根据 [AV/C 设备 id](av-c-device-identifiers.md)中描述的格式， *Avc.sys* 用于生成虚拟子区域设备标识符字符串的格式如下所示：

-   硬件标识符

<a href="" id="vavc-vendor-model-subunittype-subunitid"></a>**VAVC \\ *供应商* & *型号* & *SubunitType*& * SubunitID***  
此硬件标识符是最完整的，但这种情况很少在 INF 文件中指定，因为次级标识符 (设备标识符的最后一个符号分隔部分，而不是通常感兴趣) 。

-   兼容标识符

<a href="" id="vavc-subunittype-subunitid"></a>**VAVC \\ *SubunitType*& * SubunitID***  
虽然 *Avc.sys* 未为对等子单元连接提供这种兼容标识符，但它确实为虚拟子单元连接提供了这种兼容标识符。

<a href="" id="vavc-subunittype"></a>**VAVC \\ * SubunitType***  
虽然 *Avc.sys* 未为对等子单元连接提供这种兼容标识符，但它确实为虚拟子单元连接提供了这种兼容标识符。

<a href="" id="vavc-generic"></a>**VAVC \\ 泛型**  
"通用" 单元驱动程序在其 INF 文件中包含此项。

 

 




