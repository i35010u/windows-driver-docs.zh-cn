---
title: 创建组件以使用 SAN
description: 创建组件以使用 SAN
ms.assetid: b7405eda-734e-43f0-b0fe-747a06766291
keywords:
- 系统区域网络 WDK，创建组件
- SAN WDK，创建组件
- 传输驱动程序 WDK San
- 数据传输 WDK San
- 将数据 WDK San 传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46f6589723efba3e4100dd1e6904894a97b2595c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357364"
---
# <a name="creating-components-for-using-a-san"></a>创建组件以使用 SAN





Windows 套接字应用程序可以受益于使用系统区域网络 (SAN)。 若要使用 SAN，这些应用程序必须具有 SAN 服务提供程序 DLL 和代理驱动程序为该 DLL。

若要使用特定 SAN 来传输数据，您还需要可靠传输该 SAN。 如果在 SAN NIC 硬件中完全实现可靠传输，则为 SAN 需要传输驱动程序。 如有必要，SAN 传输驱动程序 SAN NIC 供应商指定，并且其基础 SAN 代理驱动程序和基础 SAN NIC 的专用接口通过与其通信。

有关实现 SAN 服务提供程序 DLL 和其代理驱动程序的信息，请参阅[Windows 套接字直接](windows-sockets-direct.md)。 但请注意，本部分中未指定如何编写 SAN 传输驱动程序。

需要 NDIS 微型端口驱动程序将必须通过以太网、 ATM 或另一个 SAN 等特定 SAN 以外的网络流的数据传输。 TCP/IP 使用 NDIS 微型端口驱动程序将数据发送到 SAN NIC 和此类网络上。

有关实施微型端口和传输驱动程序的信息，请参阅*微型端口驱动程序*并[TDI 传输和及其客户端](https://msdn.microsoft.com/library/windows/hardware/ff565587)。

 

 





