---
title: 转换为 SAN 本机地址
description: 转换为 SAN 本机地址
keywords:
- 代理驱动程序 WDK San，本机地址转换
- SAN 代理驱动程序 WDK，本机地址转换
- 本机地址转换 WDK San
- 翻译本机地址 WDK San
- AF_INET 解决 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88c1e6e07eb66c58d82f0981956136241f29a805
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815861"
---
# <a name="translating-to-a-san-native-address"></a>转换为 SAN 本机地址





Windows 套接字交换机始终使用 [WSK 地址系列](ws2def-h.md) 来与 san 服务提供程序（而不是 san 的本机地址系列）交互。 因此，SAN 服务提供程序的代理驱动程序必须在 WSK 地址族与本机地址之间进行相应的转换。

代理驱动程序使用 TDI 即插即用 (PnP) 通知来维护分配给其控制下的每个 NIC 的 IP 地址列表，如 [注册 SAN NIC 通知](registering-for-san-nic-notifications.md)中所述。 代理驱动程序使用此列表在本机 SAN 地址和 IP 地址之间进行转换。

代理驱动程序接收来自其包含 IP 地址的 SAN 服务提供商的请求。 例如，这些请求包括绑定到特定 NIC 的请求和连接到远程对等方的请求。 代理驱动程序必须转换为本机 SAN 地址才能完成这些请求。 代理驱动程序还会接收来自远程对等方的传入连接请求，这些请求包含那些远程对等方的 SAN 本机地址。 代理驱动程序必须转换为这些远程对等节点的 IP 地址，才能完成这些请求。

**注意**  Windows Vista 之后的 Microsoft Windows 版本不支持 TDI。 请改用 [Windows 筛选平台](/windows-hardware/drivers/ddi/_netvista/) 或 [Winsock 内核](/windows-hardware/drivers/ddi/_netvista/) 。

 

 

