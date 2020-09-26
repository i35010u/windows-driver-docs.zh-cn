---
title: 智能卡读卡器设备设计指南
description: 有关为智能卡读卡器设备开发驱动程序的设计指南。
ms.assetid: e0827569-6c76-42a1-b94f-29235646519f
keywords:
- 智能卡驱动程序 WDK
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 67947a5732d1dadc60e54b90d3d7a1d33da4df1f
ms.sourcegitcommit: ee3e2259aafc844cc43cce62299a72649cf89212
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2020
ms.locfileid: "91353598"
---
# <a name="smart-card-reader-devices-design-guide"></a>智能卡读卡器设备设计指南

有关为智能卡读卡器设备开发驱动程序的设计指南。

## <a name="in-this-section"></a>在本节中

|主题|说明|
|----|----|
|[智能卡驱动程序环境](smart-card-driver-environment.md)|描述智能卡读卡器驱动程序的标准环境。|
|[智能卡读卡器驱动程序中的 IOCTL 请求管理](management-of-ioctl-requests-in-a-smart-card-reader-driver.md)|说明读卡器驱动程序管理 IOCTL 请求的方式、回调例程机制的工作方式以及读卡器驱动程序必须执行哪些操作来初始化其回调例程。|
|[WDM 读卡器驱动程序](wdm-reader-driver.md)|列出 WDM 读卡器驱动程序所需的例程。|
|[智能卡微型驱动程序](smart-card-minidrivers.md)|智能卡微型驱动程序提供了一种更简单的替代方法，用于通过封装来自智能卡微型驱动程序开发人员的大多数复杂加密操作来开发旧式加密服务提供程序 (CSP)。|
|[智能卡读卡器状态](smart-card-reader-states.md)|列出智能卡读卡器状态及其含义的表。|
|[安装智能卡读卡器驱动程序](installing-smart-card-reader-drivers.md)|提供特定于 Windows 版智能卡读卡器驱动程序的安装信息。|
|[注册 WDM 智能卡读卡器驱动程序](registering-a-wdm-smart-card-reader-driver.md)|提供注册 WDM 智能卡读卡器驱动程序所需的注册表值及其说明。|
|[在注册表中启用智能卡事件日志记录](enabling-smart-card-event-logging-in-the-registry.md)|用于事件日志记录的注册表值名称和注册表值的内容。|
|[智能卡读卡器的 WDM 设备名称](wdm-device-names-for-smart-card-readers.md)|有关遵循 Windows 操作系统中设备名称命名约定的说明。|
|[智能卡驱动程序调试](smart-card-driver-debugging.md)|介绍调试功能的智能卡驱动程序库支持。|
|[规范和资源](specifications-and-resources.md)|若要使用 Microsoft Windows 操作系统中的智能卡支持，智能卡读卡器和卡应当符合 ICC 和个人电脑系统的互操作性规范。 智能卡读卡器和设备驱动程序还应当符合即插即用标准。</p></td>
</tr>
</tbody>
</table>

 

 

 





