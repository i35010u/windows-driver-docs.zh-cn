---
title: 人机接口设备 (HID) 驱动程序示例
description: 此目录中的驱动程序示例用于编写自定义你的设备的 HID 驱动程序提供一个起始点。
ms.assetid: 38C52EAD-9DC6-4575-A9FF-1472FDDC2702
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e57fee93bed6df65f70880218801673980d87812
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545059"
---
# <a name="human-interface-devices-hid-driver-samples"></a>人机接口设备 (HID) 驱动程序示例


此目录中的驱动程序示例用于编写自定义你的设备的 HID 驱动程序提供一个起始点。

## <a name="human-interface-devices-hid"></a>人机接口设备 (HID)


| 示例名称         | 解决方案                                                     | 描述                                                                                                                                                                                                                                                                                                                                 |
|---------------------|--------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| KMDF HID 筛选器     | [firefly](https://go.microsoft.com/fwlink/p/?LinkId=620192)   | HID 设备的筛选器驱动程序。 演示如何编写筛选器驱动程序，以及此示例演示如何使用远程 I/O 目标接口在内核模式下打开 HID 集合并发送 IOCTL 请求，以设置和获取功能的报表，以及如何应用程序可以使用 WMI 接口发送为筛选器驱动程序的命令。 |
| HClient 应用程序 | [hclient](https://go.microsoft.com/fwlink/p/?LinkId=617730)   | 演示如何编写与符合 HID 设备类规范的 HID 设备通信的用户模式下客户端应用程序。                                                                                                                                                                                               |
| HIDUSBFX2           | [hidusbfx2](https://go.microsoft.com/fwlink/p/?LinkId=620190) | 演示映射到 HID 设备的非-HID USB 设备。                                                                                                                                                                                                                                                                               |
| UMDF HID 微型驱动程序 | [vhidmini2](https://go.microsoft.com/fwlink/p/?LinkId=617731) | 演示如何编写使用用户模式驱动程序框架 (UMDF) HID 微型驱动程序的示例。                                                                                                                                                                                                                                           |

 

 

 




