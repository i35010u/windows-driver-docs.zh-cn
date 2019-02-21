---
title: Windows 便携式设备 (WPD) 驱动程序示例
description: 此目录中的驱动程序示例编写你的设备的自定义 WPD 驱动程序提供一个起始点。
ms.assetid: 5EB5B820-A29A-4A93-BBB9-6F4CDF101E3B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c36c16098cdc7d8b85252e2032ff034648d4561
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555283"
---
# <a name="windows-portable-device-wpd-driver-samples"></a>Windows 便携式设备 (WPD) 驱动程序示例


此目录中的驱动程序示例编写你的设备的自定义 WPD 驱动程序提供一个起始点。

## <a name="windows-portable-device-wpd"></a>Windows 便携设备 (WPD)


| 示例名称                               | 解决方案                                                                   | 描述                                                                                                                                                                                                                                                           |
|-------------------------------------------|----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| WPD 基本硬件示例驱动程序 (UMDF 1) | [WpdBasicHardwareDriver](https://go.microsoft.com/fwlink/p/?LinkId=620318)  | WPD 示例驱动程序支持与视差 BS2 可编程微控制器的九个传感器设备。                                                                                                                                              |
| Hello World 示例                       | [WpdHelloWorldDriver](https://go.microsoft.com/fwlink/p/?LinkId=618008)     | 此示例驱动程序支持四个对象： 一个设备对象、 存储对象、 一个文件夹和文件对象。 每个对象支持一的组属性。                                                                                                            |
| 多传输驱动程序                    | [WpdMultiTransportDriver](https://go.microsoft.com/fwlink/p/?LinkId=618009) | 演示如何可以扩展为支持多个传输协议的设备 WpdHelloWorldDriver。 传输已对其便携式设备与计算机进行通信的协议。 示例的传输包括 Internet 协议 (IP)、 蓝牙和 USB。 |
| WPD 服务示例驱动程序                 | [WpdServiceSampleDriver](https://go.microsoft.com/fwlink/p/?LinkId=618010)  | 演示如何扩展 WpdHelloWorldDriver 示例，以便它支持使用联系人设备服务模拟的设备。                                                                                                                                      |
| WUDF 驱动程序                               | [WpdWudfSampleDriver](https://go.microsoft.com/fwlink/p/?LinkId=618011)     | 一个全面的 WPD 示例驱动程序演示了 WPD 设备驱动程序接口 (DDI) 的几乎所有方面。                                                                                                                                                        |

 

 

 




