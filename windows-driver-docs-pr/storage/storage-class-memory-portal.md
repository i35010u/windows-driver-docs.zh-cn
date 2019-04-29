---
title: 存储类内存
description: 若要支持特定于设备的类的 Windows 中的存储驱动程序堆栈和平台固件之间的通信，Microsoft 定义了特定于设备的方法 (\_DSM) 可用于存储驱动程序。
ms.assetid: e4f354d0-f292-4dc2-a7e3-edd8dfa63b90
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: abdc8fa4f230f816119a4f21f73b7371b1241909
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360864"
---
# <a name="storage-class-memory"></a>存储类内存


若要支持特定于设备的类的 Windows 中的存储驱动程序堆栈和平台固件之间的通信，Microsoft 定义了特定于设备的方法 (\_DSM) 可用于存储驱动程序。

\_字节可寻址能源支持的函数类 (函数接口 1) 的 DSM 接口设计为映射到 JEDEC 字节可寻址能源支持接口标准，以便最大程度减少 BIOS 复杂性。 它提供公共基础的报告设备功能和功能，以便操作系统软件可以通过相同的机制与各种实现交互。 此外，它允许对通过 I2C 寄存器访问特定于供应商的功能的支持。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[存储驱动程序设计指南](https://go.microsoft.com/fwlink/p/?LinkId=798409)

[JEDEC 字节可寻址能源支持接口 NVDIMM 特定于设备的方法 (\_DSM)](jedec-byte-addressable-energy-backed-interface-nvdimms-device-specific-method---dsm-.md)

[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






