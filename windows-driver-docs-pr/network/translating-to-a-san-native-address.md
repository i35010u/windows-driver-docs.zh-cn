---
title: 转换为 SAN 本机地址
description: 转换为 SAN 本机地址
ms.assetid: 959c66f2-4801-47d5-9e80-f18f17057e23
keywords:
- 代理驱动程序 WDK San、 本机地址转换
- SAN 代理驱动程序 WDK，本机地址转换
- 本机地址转换 WDK San
- 转换本机地址分配 WDK San
- AF_INET 地址 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0de5e3c18e16fc96465ca7b7c425149a2c8e2a8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368455"
---
# <a name="translating-to-a-san-native-address"></a>转换为 SAN 本机地址





始终使用 Windows 套接字，切换[WSK 地址系列](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt808757(v=vs.85))与 SAN 服务提供商，不使用 SAN 的本机地址系列进行交互。 因此，SAN 服务提供程序的代理驱动程序必须将转换 WSK 地址系列和本机地址之间相应地。

代理驱动程序将使用 TDI Plug and Play (PnP) 通知保持分配给其控制下的每个 NIC 的 IP 地址的列表，如中所述[注册 SAN NIC 通知](registering-for-san-nic-notifications.md)。 代理驱动程序使用此列表本机 SAN 地址和 IP 地址之间进行转换。

代理驱动程序从其 SAN 服务提供程序包含 IP 地址接收请求。 这些请求包括，例如，要将绑定到特定 NIC 的请求和连接到远程对等方的请求。 代理驱动程序必须将转换为本机 SAN 地址来完成这些请求。 代理驱动程序还会从包含这些远程对等节点的 SAN 本机地址的远程对等节点接收传入连接请求。 代理驱动程序必须将转换到这些远程对等节点来完成这些请求的 IP 地址。

**请注意**  TDI 将不支持在 Microsoft Windows 版本在 Windows Vista 后。 使用[Windows 筛选平台](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)或[Winsock 内核](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)相反。

 

 

 





