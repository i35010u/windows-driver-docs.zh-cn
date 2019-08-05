---
title: 虚拟子单元设备标识符
description: 虚拟子单元设备标识符
ms.assetid: c2018560-f9f4-4aaa-b2b2-8ac5195b892f
keywords:
- AV/C WDK 标识符
- 标识符 WDK AV/C
- 设备 Id WDK AV/C
- Avc.sys 功能驱动程序 WDK，标识符
- 虚拟子单元设备标识符 WDK AV/C
- 子单元支持 WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 096f7a783712dbb85d52f6edb7d4bc8042c1d487
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329957"
---
# <a name="virtual-subunit-device-identifiers"></a>虚拟子单元设备标识符


类似于格式的设备标识符 (ID) 字段[对等子单元连接](peer-subunit-device-identifiers.md)，格式的*Avc.sys*用来生成虚拟子单元设备标识符的字符串，根据中所述的格式[AV/C 设备 Id](av-c-device-identifiers.md)，如下所示：

-   硬件标识符

<a href="" id="vavc-vendor-model-subunittype-subunitid"></a>**VAVC\\*Vendor*&*Model*&*SubunitType*&*SubunitID***  
此硬件标识符是最完整的但因为子单元标识符 （最后一个与符号分隔的部分设备标识符） 通常不感兴趣的很少 INF 文件中指定此。

-   兼容的标识符

<a href="" id="vavc-subunittype-subunitid"></a>**VAVC\\*SubunitType*&*SubunitID***  
虽然 *Avc.sys*不提供这种类型的对等子单元连接兼容标识符，它提供这种兼容的标识符的虚拟子单元连接。

<a href="" id="vavc-subunittype"></a>**VAVC\\*SubunitType***  
虽然 *Avc.sys*不提供这种类型的对等子单元连接兼容标识符，它提供这种兼容的标识符的虚拟子单元连接。

<a href="" id="vavc-generic"></a>**VAVC\\GENERIC**  
"通用"的设备驱动程序在其 INF 文件中包括此项。

 

 




