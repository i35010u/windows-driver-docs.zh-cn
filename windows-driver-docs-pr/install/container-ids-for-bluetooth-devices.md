---
title: 蓝牙设备的容器 ID
description: 蓝牙设备的容器 ID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: caac13a5df52062e957bd9216a56d4392cab5946
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782963"
---
# <a name="container-ids-for-bluetooth-devices"></a>蓝牙设备的容器 ID


对于连接到计算机的蓝牙设备，设备的媒体访问控制 (MAC) 地址用于生成设备的容器 ID。

蓝牙总线驱动程序使用 MAC 地址作为种子值，以生成设备的唯一容器 ID。 此容器 ID 由为物理设备枚举 (*devnode*) 的每个蓝牙设备节点的蓝牙总线驱动程序提供。

Bluetooth 设备经常实现特定于蓝牙的服务。 这些服务不会安装为 Windows PnP 设备，因此没有关联的 devnodes。 但这些服务实际上是功能强大的设备实例，因为它们提供特定功能并启用与蓝牙设备的通信。

从 Windows 7 开始，操作系统会将蓝牙服务视为功能设备接口，并将这些服务与蓝牙 devnodes 用于设备进行组合。

所有蓝牙设备都必须包含 MAC 地址。 因此，蓝牙 devnodes 和服务的容器 ID 始终基于 MAC 地址值。 与 USB 设备不同，可移动设备功能绝不会用于为蓝牙设备生成容器 Id。

为了确保为每个设备生成唯一的容器 ID，蓝牙设备的开发人员必须使用唯一的 MAC 地址配置每个设备。

 

 





