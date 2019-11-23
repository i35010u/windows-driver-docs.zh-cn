---
title: 转换为 SAN 本机地址
description: 转换为 SAN 本机地址
ms.assetid: 959c66f2-4801-47d5-9e80-f18f17057e23
keywords:
- 代理驱动程序 WDK San，本机地址转换
- SAN 代理驱动程序 WDK，本机地址转换
- 本机地址转换 WDK San
- 翻译本机地址 WDK San
- AF_INET 解决 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0720b6679dbc66ecbb2e017a3ed6769359d6cde6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841777"
---
# <a name="translating-to-a-san-native-address"></a>转换为 SAN 本机地址





Windows 套接字交换机始终使用[WSK 地址系列](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt808757(v=vs.85))来与 san 服务提供程序（而不是 san 的本机地址系列）交互。 因此，SAN 服务提供程序的代理驱动程序必须在 WSK 地址族与本机地址之间进行相应的转换。

代理驱动程序使用 TDI 即插即用（PnP）通知来维护分配给其控制的每个 NIC 的 IP 地址列表，如[注册 SAN NIC 通知](registering-for-san-nic-notifications.md)中所述。 代理驱动程序使用此列表在本机 SAN 地址和 IP 地址之间进行转换。

代理驱动程序接收来自其包含 IP 地址的 SAN 服务提供商的请求。 例如，这些请求包括绑定到特定 NIC 的请求和连接到远程对等方的请求。 代理驱动程序必须转换为本机 SAN 地址才能完成这些请求。 代理驱动程序还会接收来自远程对等方的传入连接请求，这些请求包含那些远程对等方的 SAN 本机地址。 代理驱动程序必须转换为这些远程对等节点的 IP 地址，才能完成这些请求。

**请注意**，在 Windows Vista 之后的 Microsoft windows 版本中不支持  TDI。 请改用[Windows 筛选平台](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)或[Winsock 内核](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

 

 

 





