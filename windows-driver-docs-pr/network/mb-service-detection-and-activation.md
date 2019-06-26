---
title: MB 服务检测和激活
description: MB 服务检测和激活
ms.assetid: 7c53528b-722d-44a1-9eac-ee1fe89f21f3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a551ef9d08a4086c5e2c68c43516ebbbe25357ed
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374015"
---
# <a name="mb-service-detection-and-activation"></a>MB 服务检测和激活


本主题介绍的过程来检测的 MB 设备是否必须激活，其服务以及如何获取对提供程序的网络访问权限。

### <a name="service-activation-detection"></a>服务激活检测

微型端口驱动程序可以确定是否必须在两种方法中执行服务激活：

-   对于基于 CDMA 的设备，在北美或其他位置中的未使用 U RIM，应该有一个标志以指示激活状态在设备上。 微型端口驱动程序应该能够在初始化期间检测到激活状态，而无需联系提供程序网络。 微型端口驱动程序应自动执行服务激活，当设备首次连接到家庭网络无线。 激活完成后，微型端口驱动程序应清除标志，以便它们不需要执行再次激活服务。

    微型端口驱动程序通过发送，MB 服务告知服务激活进度[ **NDIS\_状态\_WWAN\_准备\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info)在 MB 设备初始化过程中的通知。 或者，若要确定服务激活状态，该服务可能会发送[OID\_WWAN\_准备\_信息](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info)微型端口驱动程序的查询请求。 在这两种情况下，初始的就绪状态应**WwanReadyStateNotActivated**。 服务已激活后，微型端口驱动程序应继续初始化过程，并为设备就绪状态更改通知服务。

-   对于基于 GSM 的设备，没有任何常规方法来检测设备是否必须激活其服务。 微型端口驱动程序可以实现自己专有的方法，特定于其运营商，以执行服务检测和激活。

### <a name="mb-service-activation"></a>MB 服务激活

服务激活是指激活 MB 服务订阅，以便设备能够提供程序的网络访问权限的过程。 MB 服务未配备有服务激活逻辑，因为必须由微型端口驱动程序和/或第三方软件执行的确切的激活过程，因为实际激活过程从移动电话技术而异，通常是自定义为不同的提供程序网络。 服务激活可以自动，或手动或这两者的组合。 微型端口驱动程序应只需执行的每个新订阅的服务激活一次。

有关服务检测和激活的详细信息，请参阅[OID\_WWAN\_服务\_激活](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-service-activation)。

 

 





