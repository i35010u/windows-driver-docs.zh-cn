---
title: MB 服务检测和激活
description: MB 服务检测和激活
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a01028a2a9e8a19713af60b65383cd120c87207b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839883"
---
# <a name="mb-service-detection-and-activation"></a>MB 服务检测和激活


本主题介绍了检测 MB 设备是否必须激活服务的过程，以及如何获取访问接口网络的访问权限。

### <a name="service-activation-detection"></a>服务激活检测

微型端口驱动程序可以通过以下两种方式来确定它们是否必须执行服务激活：

-   对于基于 CDMA 的设备，在北美或未使用 U 边缘的其他位置中，在设备上应有一个标志来指示激活状态。 小型端口驱动程序应能够在初始化期间检测激活状态，而无需联系提供程序网络。 当设备首次连接到家庭网络时，微型端口驱动程序应自动执行服务激活。 完成激活后，微型端口驱动程序应该清除标志，这样它们就不需要再次执行服务激活。

    微型端口驱动程序通过在 MB 设备初始化期间发送 [**NDIS \_ 状态 \_ WWAN \_ 就绪 \_ 信息**](./ndis-status-wwan-ready-info.md) 通知来通知 MB 服务的服务激活进度。 或者，若要确定服务激活状态，该服务可能会向微型端口驱动程序发送 [OID \_ WWAN \_ 就绪 \_ 信息](./oid-wwan-ready-info.md) 查询请求。 在这两种情况下，初始就绪状态应为 **WwanReadyStateNotActivated**。 激活服务后，微型端口驱动程序应恢复初始化过程，并在设备就绪状态发生更改时通知服务。

-   对于基于 GSM 的设备，没有用于检测是否必须激活设备服务的一般方法。 微型端口驱动程序可以实现其自己的专用方法（特定于其运营商）来执行服务检测和激活。

### <a name="mb-service-activation"></a>MB 服务激活

服务激活是指激活 MB 服务订阅的过程，以便设备可以访问提供程序的网络。 MB 服务未配备服务激活逻辑，因为完全激活过程必须由微型端口驱动程序和/或第三方软件执行，因为实际激活过程因蜂窝技术而异，通常针对不同的提供商网络进行自定义。 服务激活可以是自动、手动或二者的组合。 小型端口驱动程序应该只需要为每个新订阅执行一次服务激活。

有关服务检测和激活的详细信息，请参阅 [OID \_ WWAN \_ 服务 \_ 激活](./oid-wwan-service-activation.md)。

 

