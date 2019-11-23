---
title: 注册 SAN NIC 通知
description: 注册 SAN NIC 通知
ms.assetid: 6a630e7c-3b1a-4f4a-b808-f6b4e2315a42
keywords:
- NIC 通知 WDK San
- 代理驱动程序 WDK San，NIC 通知
- SAN 代理驱动程序 WDK、NIC 通知
- 注册 NIC 通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8343c698a8589d2a1b34a56b53c07a31575f46a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842073"
---
# <a name="registering-for-san-nic-notifications"></a>注册 SAN NIC 通知





当代理驱动程序收到来自其关联的 SAN 服务提供商的请求以提供分配给驱动程序控件下的 Nic 的 IP 地址列表时，驱动程序将确定此列表并将其传递给提供程序。

为了获取这些 IP 地址，代理驱动程序必须注册传输驱动程序接口（TDI）才能接收地址更改通知。 代理驱动程序调用[**TdiRegisterPnPHandlers**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565062(v=vs.85))函数。 在此调用中，此代理驱动程序将指针传递到 TDI\_CLIENT\_INTERFACE\_INFO 结构的**AddAddressHandlerV2**和**DelAddressHandlerV2**成员中的回调函数，以指定用于添加和删除地址的回调函数。 成功返回**TdiRegisterPnPHandlers**函数后，TDI 会使用地址添加回调立即指示所有当前处于活动状态的代理驱动程序的网络地址。 指示包含这些地址所绑定到的设备的网络地址和标识符。

当 TDI 调用这些回调函数中的任何一个来指示地址添加或删除时，代理驱动程序需要以下参数：

<a href="" id="address"></a>*地址*  
一个指针，指向 TA\_地址结构，该结构描述分配给 NIC 或从中删除的网络地址。 对于 TCP/IP，此指针实际上是指向 TA\_地址\_IP 结构的指针。

<a href="" id="devicename"></a>*DeviceName*  
指向一个 Unicode 字符串的指针，该字符串标识与该地址关联的传输到 NIC 的绑定。 对于 TCP/IP，Unicode 字符串具有以下格式： \\设备\\Tcpip\_{NIC-GUID}，其中 NIC-GUID 是网络配置子系统分配给 NIC 的全局唯一标识符。

前面的结构定义在 tdi .h 头文件中定义。 前面的注册和回调函数在 tdikrnl 头文件中定义。 这些头文件在 Microsoft Windows 驱动程序开发工具包（DDK）和 Windows 驱动程序工具包（WDK）中提供。 有关 TDI 即插即用（PnP）通知的详细信息，请参阅[Tdi 客户端回调](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565081(v=vs.85))和[Tdi 客户端事件和 PnP 通知处理程序](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565082(v=vs.85))。

系统启动时，TDI 会调用代理驱动程序的地址添加回拨，以指示所有当前活动的 IP 地址。 当 TCP/IP 传输协议向 TDI 注册新的 IP 地址时，TDI 还会调用此回调。 代理驱动程序的 IP 地址列表中只包含分配给代理驱动程序的 Nic 的地址。 如果驱动程序无法在*DeviceName*识别 NIC，则驱动程序的地址添加回调应立即返回控制权。

当 TCP/IP 传输协议向 TDI 表明已删除 NIC 时，TDI 会调用代理驱动程序的地址删除回调。 如果 NIC 的 IP 地址属于某个代理驱动程序的 Nic，则代理驱动程序将从该列表中删除该 IP 地址。

**请注意**，在 Windows Vista 之后的 Microsoft windows 版本中不支持  TDI。 请改用[Windows 筛选平台](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)或[Winsock 内核](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

 

 

 





