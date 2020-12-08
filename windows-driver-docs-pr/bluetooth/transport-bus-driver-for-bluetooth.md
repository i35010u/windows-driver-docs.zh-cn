---
title: 蓝牙的传输总线驱动程序
description: 下面的示例系统关系图描述了用于支持多功能控制器的驱动程序堆栈，使用 UART 作为其传输。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ece6c693be4c4398eb7afe73dfd26c84a0cc282e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789161"
---
# <a name="transport-bus-driver-for-bluetooth"></a>蓝牙的传输总线驱动程序


下面的示例系统关系图描述了用于支持多功能控制器的驱动程序堆栈，使用 UART 作为其传输。

![蓝牙示例传输总线驱动程序](images/bthsampletransportbusdriver.png)

支持蓝牙功能的设备堆栈包含两个层：

1.  用于支持多功能外围设备的 **串行总线驱动程序层** ，在关系图中 (或所谓的 "combo" 芯片，以支持蓝牙和 FM) 。
2.  基于由串行总线驱动程序创建的子 PDO 加载的 **蓝牙核心驱动程序层** ，以支持蓝牙功能。

以下主题讨论了电源管理中这两个层的角色：

-   [蓝牙核心驱动程序层和支持的功率转换](bluetooth-core-driver-layer-and-supported-power-transitions.md)
-   [串行总线驱动程序层](serial-bus-driver-layer.md)

 

 





