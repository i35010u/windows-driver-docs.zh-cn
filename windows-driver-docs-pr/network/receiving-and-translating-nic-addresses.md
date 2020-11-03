---
title: 接收和转换 NIC 地址
description: 接收和转换 NIC 地址
ms.assetid: c7171a4d-cc77-427e-8d23-8811f650e543
keywords:
- Windows 套接字直通 WDK，初始化 SAN 使用情况
- 正在初始化 SAN 使用情况
- NIC 地址转换 WDK San
- 转换 NIC 地址 WDK San
- 接收 San 的 NIC 地址
- 解决 WDK San
- 删除-地址通知 WDK San
- 添加地址通知 WDK San
- 通知 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5ad04ce07695c2e7afd8a74391fbf4e771def11
ms.sourcegitcommit: 409dd20db50c58b817ef985048fb7aab952cb0ad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93244854"
---
# <a name="receiving-and-translating-nic-addresses"></a>接收和转换 NIC 地址





与 SAN 服务提供商和 SAN Nic 交互时，Windows 套接字交换机始终使用包含 IP 地址的 [WSK 地址系列](ws2def-h.md)。 此开关不使用 SAN 的本机地址系列。 因此，SAN 服务提供商必须使用其关联的代理驱动程序来检索分配给其 Nic 的 IP 地址的列表。 在与其代理驱动程序交互时，SAN 服务提供程序使用这些 IP 地址。 代理驱动程序必须在 IP 地址和本机地址之间进行转换。

在初始化期间，代理驱动程序通常为地址更改通知注册传输驱动程序接口 (TDI) 。 所有即插即用 (PnP) 识别的传输，包括 TCP/IP，并通过 TDI 向注册了此类通知的客户端提供地址更改通知。

**注意**  Windows Vista 之后的 Microsoft Windows 版本不支持 TDI。 请改用 [Windows 筛选平台](/windows-hardware/drivers/ddi/_netvista/) 或 [Winsock 内核](/windows-hardware/drivers/ddi/_netvista/) 。

 

### <a name="registering-for-address-change-notification"></a>注册地址更改通知

在初始化期间，代理驱动程序会调用 [**TdiRegisterPnPHandlers**](/previous-versions/windows/hardware/network/ff565062(v=vs.85)) 函数来注册地址更改通知。 在此调用中，代理驱动程序将指针传递到回调函数，以便在 TDI **AddAddressHandlerV2** **DelAddressHandlerV2** \_ 客户端 \_ 接口信息结构的 AddAddressHandlerV2 和 DelAddressHandlerV2 成员中添加和删除地址 \_ 。 在代理驱动程序注册接收这些通知后，TDI 会立即使用添加地址回拨指示所有当前处于活动状态的网络地址。

TDI 将以下参数传递给代理驱动程序的添加地址或删除地址回调函数：

<a href="" id="address"></a>*地址*  
一个指针， \_ 它指向描述分配给 NIC 或从中删除的网络地址的 TA 地址结构。 对于 TCP/IP，此指针实际上是指向 TA \_ 地址 \_ IP 结构的指针。

<a href="" id="devicename"></a>*DeviceName*  
指向一个 Unicode 字符串的指针，该字符串标识与该地址关联的传输到 NIC 的绑定。 如果是 TCP/IP，则 Unicode 字符串具有以下格式：

\\设备 \\ Tcpip \_ {NIC-GUID}

其中 NIC-GUID 是由网络配置子系统分配给 NIC 的全局唯一标识符。

前面的结构定义在 tdi .h 头文件中定义。 前面的注册和回调函数在 tdikrnl 头文件中定义。 这些头文件在 Microsoft Windows 驱动程序开发工具包 (DDK) 和 Windows 驱动程序工具包 (WDK) 中提供。 [Tdi 客户端回调](/previous-versions/windows/hardware/network/ff565081(v=vs.85))和[Tdi 客户端事件和 PnP 通知处理程序](/previous-versions/windows/hardware/network/ff565082(v=vs.85))中包含有关 tdi PnP 通知的详细信息。

**注意**  Windows Vista 之后的 Microsoft Windows 版本不支持 TDI。 请改用 [Windows 筛选平台](/windows-hardware/drivers/ddi/_netvista/) 或 [Winsock 内核](/windows-hardware/drivers/ddi/_netvista/) 。

 

### <a name="maintaining-a-list-of-ip-addresses"></a>维护 IP 地址列表

SAN 服务提供商的代理驱动程序使用添加地址和删除地址通知来维护分配给其控制下的每个 NIC 的 IP 地址的列表。 代理驱动程序使用此列表，通过 TCP/IP 传输和本机 SAN 地址在分配到 SAN NIC 的一个或多个 IP 地址之间进行转换。 代理驱动程序还必须提供设备控制例程，使分配给 NIC 的 IP 地址的列表在交换机进行 SIO \_ 地址 \_ 列表 \_ 查询控制代码查询时可用于 Windows 套接交换机。 代理驱动程序的 **DriverEntry** 例程必须指定此设备控制例程的入口点。

Windows 套接字交换机维护分配给每个 SAN NIC 的所有 IP 地址的列表。 若要检索此 "包含列表" 的 IP 地址，交换机将调用每个 SAN 服务提供程序的 [**WSPIoctl**](/previous-versions/windows/hardware/network/ff566296(v=vs.85)) 函数，同时传递 SIO \_ 地址 \_ 列表 \_ 查询控制代码。 接下来，每个 SAN 服务提供程序将查询其关联的代理驱动程序，以获取分配给其 SAN Nic 的单个 IP 地址列表。 在开关收到地址更改的通知后，它会再次查询每个 SAN 服务提供程序以获取每个单独列表中的更新。

 

