---
title: 关于存储类内存
description: 为了支持 Windows 中的存储驱动程序堆栈和平台固件之间的特定于设备的通信，Microsoft 定义了可用于存储驱动程序的特定于设备的方法（_DSM）。
ms.assetid: e4f354d0-f292-4dc2-a7e3-edd8dfa63b90
ms.localizationpriority: medium
ms.date: 12/15/2019
ms.openlocfilehash: 1e47c9a6b6fea8200241e624c1ae5ba5ce3667b6
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606537"
---
# <a name="about-storage-class-memory"></a>关于存储类内存

为了支持 Windows 中的存储驱动程序堆栈和平台固件之间的特定于设备的通信，Microsoft 定义了可用于存储驱动程序的特定于设备的方法（_DSM）。

用于字节可寻址的受支持能量的函数类（函数接口1）的 _DSM 接口旨在映射到 JEDEC Byte 可寻址的支持电源的接口标准，以最大程度地减少 BIOS 复杂性。 它提供了报表设备功能 & 功能的常见基础，使 OS 软件可以通过相同的机制与各种实现交互。 此外，它还允许通过访问 I2C 寄存器来支持供应商特定的功能。 支持 JEDEC Byte 可寻址能耗支持的接口标准的 NVDIMM-N 具有一个函数类，该函数类支持字节可寻址的能量（0x1）和函数接口值0x1。

## <a name="related-topics"></a>相关主题

[存储驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/storage)

[JEDEC Byte 可寻址能量支持的函数类的 _DSM 接口（Function Interface 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)
