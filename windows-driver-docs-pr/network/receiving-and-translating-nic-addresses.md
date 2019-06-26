---
title: 接收和转换 NIC 地址
description: 接收和转换 NIC 地址
ms.assetid: c7171a4d-cc77-427e-8d23-8811f650e543
keywords:
- Windows 套接字直接 WDK，初始化 SAN 使用率
- 初始化 SAN 使用率
- NIC 地址转换 WDK San
- 转换 NIC 地址 WDK San
- 为接收 NIC 地址 San
- 地址 WDK San
- 删除地址通知 WDK San
- 添加地址通知 WDK San
- 通知 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eecfd5a8d7decc35e3d75ba08ea521708c9c7d6a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368471"
---
# <a name="receiving-and-translating-nic-addresses"></a>接收和转换 NIC 地址





始终使用 Windows 套接字，切换[WSK 地址系列](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt808757(v=vs.85))，其中包含 IP 地址与 SAN 服务提供商和 SAN Nic 交互时发生。 此开关不使用 SAN 的本机地址族。 因此，SAN 服务提供程序必须使用其关联的代理的驱动程序来检索分配给其 Nic 的 IP 地址的列表。 SAN 服务提供商与及其代理驱动程序进行交互时使用这些 IP 地址。 代理驱动程序必须将 IP 地址与本机地址之间转换。

在初始化期间，代理驱动程序通常注册传输驱动程序接口 (TDI) 地址更改通知。 所有插即用 (PnP) 注意传输，包括 TCP/IP，都提供通过 TDI 向此类通知已注册的客户端的地址更改通知。

**请注意**  TDI 将不支持在 Microsoft Windows 版本在 Windows Vista 后。 使用[Windows 筛选平台](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)或[Winsock 内核](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)相反。

 

### <a name="registering-for-address-change-notification"></a>正在注册的地址更改通知

在初始化期间，代理驱动程序调用[ **TdiRegisterPnPHandlers** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565062(v=vs.85))函数以注册地址更改通知。 在此调用中，代理驱动程序将指针传递给回调函数以获取地址添加和删除操作中的**AddAddressHandlerV2**并**DelAddressHandlerV2** TDI 成员\_客户端\_接口\_信息结构。 代理驱动程序注册以接收这些通知后，TDI 立即指示使用添加地址回调的所有当前处于活动状态的网络地址。

TDI 将以下参数传递给代理驱动程序添加地址或删除地址回调函数：

<a href="" id="address"></a>*地址*  
指向 TA\_地址结构描述的网络地址分配到或从 NIC 中删除 对于 TCP/IP，此指针是实际指向 TA\_地址\_IP 结构。

<a href="" id="devicename"></a>*DeviceName*  
标识该地址与之关联的传输 NIC 绑定的 Unicode 字符串指针。 对于 TCP/IP，Unicode 字符串采用以下格式：

\\Device\\Tcpip\_{NIC-GUID}

其中 NIC GUID 是分配给 NIC 的网络配置子系统的全局唯一标识符

前面的结构定义 tdi.h 标头文件中定义。 Tdikrnl.h 标头文件中定义的前面注册和回调函数。 这些标头文件是在 Microsoft Windows 驱动程序开发工具包 (DDK) 和 Windows Driver Kit (WDK) 中可用。 有关 TDI 即插即用通知的详细的信息包含在[TDI 客户端回调](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565081(v=vs.85))并[TDI 客户端事件和即插即用通知处理程序](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565082(v=vs.85))。

**请注意**  TDI 将不支持在 Microsoft Windows 版本在 Windows Vista 后。 使用[Windows 筛选平台](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)或[Winsock 内核](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)相反。

 

### <a name="maintaining-a-list-of-ip-addresses"></a>维护 IP 地址的列表

SAN 服务提供商的代理驱动程序使用添加地址和删除地址通知来维护分配给其控制下的每个 NIC 的 IP 地址的列表。 代理驱动程序使用此列表将一个或多个 IP 地址分配给 SAN NIC 的 TCP/IP 传输和本机 SAN 地址之间。 代理驱动程序还必须提供使切换开关发出 SIO 时分配给 NIC 供 Windows 套接字的 IP 地址的列表的设备控制例程\_地址\_列表\_查询控制代码查询。 代理驱动程序**DriverEntry**例程必须指定此设备控制例程的入口点。

Windows 套接字交换机维护一系列所有 IP 地址分配给每个 SAN nic。 若要检索此详尽列表的 IP 地址，此开关调用每个 SAN 服务提供商[ **WSPIoctl** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566296(v=vs.85))函数，传递 SIO\_地址\_列表\_查询控制代码。 每个 SAN 服务提供程序，反过来，查询其单独分配给其 SAN Nic 的 IP 地址的列表及其关联的代理驱动程序。 开关通知的地址更改后，它将再次查询每个单独的列表中的更新每个 SAN 服务提供程序。

 

 





