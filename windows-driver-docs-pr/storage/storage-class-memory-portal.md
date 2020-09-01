---
title: 关于存储类内存
description: 为了支持 Windows 中的存储驱动程序堆栈和平台固件之间的特定于设备的通信，Microsoft 定义了特定于设备的方法 (_DSM 可用于存储驱动程序的) 。
ms.assetid: e4f354d0-f292-4dc2-a7e3-edd8dfa63b90
ms.localizationpriority: medium
ms.date: 12/15/2019
ms.openlocfilehash: 035ffc77f688a0c221a2e6e7d19f4e0ab51a85c2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186385"
---
# <a name="about-storage-class-memory"></a>关于存储类内存

为了支持 Windows 中的存储驱动程序堆栈和平台固件之间的特定于设备的通信，Microsoft 定义了特定于设备的方法 (_DSM 可用于存储驱动程序的) 。

用于 (函数接口 1) 的用于字节可寻址能量的函数类的 _DSM 接口旨在映射到 JEDEC Byte 可寻址的支持电源的接口标准，以最大程度地减少 BIOS 复杂性。 它提供了报表设备功能 & 功能的常见基础，使 OS 软件可以通过相同的机制与各种实现交互。 此外，它还允许通过访问 I2C 寄存器来支持供应商特定的功能。 支持 JEDEC Byte 可寻址能耗支持的接口标准的 NVDIMM-N 提供了一个函数类，其中包含一个字节可寻址的能耗 (0x1) ，函数接口值为0x1。

## <a name="related-topics"></a>相关主题

[存储驱动程序设计指南](./index.md)

[可按 JEDEC 字节寻址且以能源为支持的功能类的 _DSM 接口（功能接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)