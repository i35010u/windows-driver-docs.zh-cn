---
title: WDM 与的 NDIS 微型端口驱动程序降低边缘
description: WDM 与的 NDIS 微型端口驱动程序降低边缘
ms.assetid: b371a267-c57d-4d6d-81a1-53f4b51cacea
keywords:
- 微型端口驱动程序 WDK 网络类型
- NDIS 微型端口驱动程序 WDK，类型
- WDM 较低的边缘 WDK 网络
- NDIS 微型端口驱动程序 WDK 网络的下边缘
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a13005151e58c4be3a52799a01752caf35d8b3ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519089"
---
# <a name="ndis-miniport-drivers-with-a-wdm-lower-edge"></a>WDM 与的 NDIS 微型端口驱动程序降低边缘





您可以编写用于控制设备的总线上的 NDIS 微型端口驱动程序 — 例如，通用串行总线 (USB) 或 IEEE 1394 (firewire) 总线。 这样的微型端口驱动程序必须显示在其上边缘的标准 NDIS 微型端口驱动程序接口，并为特定的总线在其下边缘使用类接口。 微型端口驱动程序与通过将 I/O 请求数据包 (Irp) 发送到总线通过其 Microsoft Windows 驱动程序模型 (WDM) 较低接口连接到总线的设备进行通信。

使用 WDM 下边缘的微型端口驱动程序必须反序列化。 有关反序列化的驱动程序的详细信息，请参阅[反序列化的 NDIS 微型端口驱动程序](deserialized-ndis-miniport-drivers.md)。

有关使用 WDM 下边缘的微型端口驱动程序的详细信息，请参阅[微型端口驱动程序使用 WDM 低界面](miniport-drivers-with-a-wdm-lower-interface.md)。

 

 





