---
title: 蓝牙设备的容器 Id
description: 蓝牙设备的容器 Id
ms.assetid: 7e9c40d9-ed19-4ad2-a749-6e3f4aaca2de
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ab6ed16e6bfb88af6a342e73d352c3ed6c4efdd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521625"
---
# <a name="container-ids-for-bluetooth-devices"></a>蓝牙设备的容器 Id


连接到计算机的蓝牙设备，设备的媒体访问控制 (MAC) 地址用于生成设备的容器 ID。

蓝牙总线驱动程序使用的 MAC 地址作为种子值生成该设备的唯一的容器 ID。 此容器 ID 提供的蓝牙设备的每个节点的蓝牙总线驱动程序 (*devnode*) 的枚举。 对于物理设备。

蓝牙设备通常会实现特定于蓝牙的服务。 这些服务未安装为 Windows 即插即用设备，因此不具有关联的 devnodes。 但是，这些服务是有效地功能的设备实例，因为它们提供特定功能，并通过蓝牙设备启用的通信。

从 Windows 7 开始，操作系统会考虑蓝牙服务，以进行功能的设备接口和这些服务，以及蓝牙 devnodes 设备进行分组。

所有蓝牙设备必须都包括 MAC 地址。 因此，Bluetooth devnodes 和服务的容器 ID 始终基于 MAC 地址值。 与不同的 USB 设备的可移动设备功能永远不会用于生成蓝牙设备的容器 Id。

若要请确保为每个设备生成 ID 的唯一容器，开发人员的蓝牙设备必须具有唯一的 MAC 地址配置的每个设备。

 

 





