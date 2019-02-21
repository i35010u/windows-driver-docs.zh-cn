---
title: 蓝牙的传输总线驱动程序
description: 示例系统中，下的图描绘了用于支持作为其传输使用 UART 的多功能控制器的驱动程序堆栈。
ms.assetid: C47FA9B7-9627-452F-8FDC-4B97FFF79E9D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5985f7d0494d23d3d3c4df51a85d3985550342a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521923"
---
# <a name="transport-bus-driver-for-bluetooth"></a>蓝牙的传输总线驱动程序


示例系统中，下的图描绘了用于支持作为其传输使用 UART 的多功能控制器的驱动程序堆栈。

![蓝牙示例传输总线驱动程序](images/bthsampletransportbusdriver.png)

设备堆栈以支持蓝牙函数由两个层组成：

1.  **串行总线驱动程序层**用于支持多功能外围设备 （或在关系图中以支持蓝牙和 FM 芯片所谓"组合"）。
2.  **蓝牙核心驱动程序层**它将被加载基于子 PDO 创建串行总线驱动程序支持蓝牙功能。

以下主题中讨论了这两个层中的电源管理的角色：

-   [蓝牙核心驱动程序层和支持的电源转换](bluetooth-core-driver-layer-and-supported-power-transitions.md)
-   [串行总线驱动程序层](serial-bus-driver-layer.md)

 

 





