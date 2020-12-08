---
title: 包含 WDM 下边缘的 NDIS 微型端口驱动程序
description: 包含 WDM 下边缘的 NDIS 微型端口驱动程序
keywords:
- 微型端口驱动程序 WDK 网络，类型
- NDIS 微型端口驱动程序 WDK，类型
- WDM 低边缘 WDK 网络
- NDIS 微型端口驱动程序的下边缘 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 013b8be4a77a8b9b4fc2f42c68574a8ef6daa9f5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801589"
---
# <a name="ndis-miniport-drivers-with-a-wdm-lower-edge"></a>包含 WDM 下边缘的 NDIS 微型端口驱动程序





可以编写用于控制总线上的设备的 NDIS 微型端口驱动程序，例如，通用串行总线 (USB) 或 IEEE 1394 (火线) 总线。 此类微型端口驱动程序必须在其上边缘公开标准 NDIS 微型端口驱动程序接口，并在其下边缘使用特定总线的类接口。 微型端口驱动程序与连接到总线的设备进行通信，方法是将 i/o 请求数据包 () Irp 发送到通过其 Microsoft Windows 驱动模型 (WDM) 低端接口的总线。

必须反序列化 WDM 下限的小型端口驱动程序。 有关反序列化驱动程序的详细信息，请参阅 [反序列化 NDIS 微型端口驱动程序](deserialized-ndis-miniport-drivers.md)。

有关具有 WDM 下边缘的微型端口驱动程序的详细信息，请参阅 [具有 Wdm 下限接口的微型端口驱动程序](miniport-drivers-with-a-wdm-lower-interface.md)。

 

 





