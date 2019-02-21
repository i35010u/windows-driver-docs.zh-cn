---
title: 通用串行总线 (USB) 驱动程序示例
description: 此目录中的驱动程序示例用于编写自定义你的设备的 USB 驱动程序提供一个起始点。
ms.assetid: 4A61F62B-9C23-4265-8AB4-D3AB45F512DF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bcd2e4c90c6a4afc75721004a8d8d7e09a1bdb0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525908"
---
# <a name="universal-serial-bus-usb-driver-samples"></a>通用串行总线 (USB) 驱动程序示例


此目录中的驱动程序示例用于编写自定义你的设备的 USB 驱动程序提供一个起始点。

## <a name="universal-serial-bus-usb"></a>通用串行总线 (USB)


| 示例名称                                                            | 解决方案                                                              | 描述                                                                                                                                                                         |
|------------------------------------------------------------------------|-----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| KMDF 总线驱动程序                                                        | [kmdf\_enumswitches](https://go.microsoft.com/fwlink/p/?LinkId=618000) | 演示如何使用 OSR USB FX2 设备 KMDF 总线驱动程序。                                                                                                          |
| OSR USB FX2 示例 KMDF 函数驱动程序                            | [kmdf\_fx2](https://go.microsoft.com/fwlink/p/?LinkId=620313)          | 演示如何执行大容量和中断数据传输到 USB 设备。 该示例专为 OSR USB FX2 学习工具包。                                              |
| USB 函数客户端驱动程序                                             | [ufxclientsample](https://go.microsoft.com/fwlink/p/?LinkId=620315)    | 演示如何创建使用 USB 函数类扩展驱动程序 (UFX) 的 Windows USB 函数控制器驱动程序框架的示例驱动程序。                                     |
| UMDF 筛选器示例上面 KMDF 功能驱动程序为 OSR USB FX2 (UMDF 1) | [umdf\_filter\_kmdf](https://go.microsoft.com/fwlink/p/?LinkId=620316) | 演示如何为上面 kmdf 上部的筛选器驱动程序加载 UMDF 筛选器驱动程序\_fx2 示例驱动程序。 该示例专为 OSR USB FX2 学习工具包。                  |
| UMDF 筛选器示例上面 UMDF 功能驱动程序为 OSR USB FX2 (UMDF 1) | [umdf\_filter\_umdf](https://go.microsoft.com/fwlink/p/?LinkId=618001) | 演示如何为上面 umdf 上部的筛选器驱动程序加载 UMDF 筛选器驱动程序\_fx2 示例驱动程序。 该示例专为 OSR USB FX2 学习工具包。                  |
| UMDF 1 函数驱动程序                                                 | [umdf\_fx2](https://go.microsoft.com/fwlink/p/?LinkId=618002)          | OSR USB FX2 设备的用户模式驱动程序框架 (UMDF 1) 驱动程序。 它包括测试应用程序和示例的设备元数据，并支持模拟和向下的空闲处理能力。 |
| UMDF 2 功能驱动程序                                                 | [umdf2\_fx2](https://go.microsoft.com/fwlink/p/?LinkId=618003)         | OSR USB FX2 设备的用户模式驱动程序框架 (UMDF 2) 驱动程序。 它包括测试应用程序和示例的设备元数据，并支持模拟和向下的空闲处理能力。 |
| Usbsamp 泛型 USB 驱动程序                                             | [usbsamp](https://go.microsoft.com/fwlink/p/?LinkId=618938)            | 演示如何执行完整的速度、 高速度、 和 SuperSpeed 传输到和从大容量和泛型的 USB 设备的同步终结点。                                    |
| USBView                                                                | [usbview](https://go.microsoft.com/fwlink/p/?LinkId=618004)            | 允许您浏览所有 USB 控制器和连接的 USB 设备在系统上的 Windows 应用程序。                                                                       |

 

 

 




