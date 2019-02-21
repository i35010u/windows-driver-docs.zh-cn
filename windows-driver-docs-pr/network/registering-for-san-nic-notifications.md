---
title: 注册 SAN NIC 通知
description: 注册 SAN NIC 通知
ms.assetid: 6a630e7c-3b1a-4f4a-b808-f6b4e2315a42
keywords:
- NIC 通知 WDK San
- 代理驱动程序 WDK San、 NIC 通知
- SAN 代理驱动程序 WDK、 NIC 通知
- 注册 NIC 通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7dbb9f789ec3f390c0f0e639101e3775efc6fcc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544178"
---
# <a name="registering-for-san-nic-notifications"></a>注册 SAN NIC 通知





当代理驱动程序收到请求时从其关联 SAN 服务提供商提供的驱动程序的控制下分配给 Nic 的 IP 地址列表时，该驱动程序确定，并将此列表传递给提供程序。

若要获取这些 IP 地址，代理驱动程序必须注册与传输驱动程序接口 (TDI) 以接收地址更改通知。 代理驱动程序调用[ **TdiRegisterPnPHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff565062)函数。 在此调用中，此代理驱动程序将指针传递给回调函数**AddAddressHandlerV2**并**DelAddressHandlerV2** TDI 成员\_客户端\_接口\_信息结构，以指定地址添加和删除操作的回调函数。 之后**TdiRegisterPnPHandlers**函数已成功返回，TDI 立即表示该代理驱动程序的所有当前处于活动状态的网络地址使用的地址添加回调。 指示包含网络地址和这些地址绑定到的设备的标识符。

每当 TDI 调用其中任一回调函数来指示地址添加或删除操作，该代理驱动程序需要以下参数：

<a href="" id="address"></a>*地址*  
指向 TA\_地址结构描述的网络地址分配到或从 NIC 中删除 对于 TCP/IP，此指针是实际上是指向 TA\_地址\_IP 结构。

<a href="" id="devicename"></a>*DeviceName*  
标识该地址与之关联的传输 NIC 绑定的 Unicode 字符串指针。 对于 TCP/IP，Unicode 字符串采用以下格式：\\设备\\Tcpip\_{NIC-GUID}，其中 NIC GUID 是分配给 NIC 的网络配置子系统的全局唯一标识符

前面的结构定义 tdi.h 标头文件中定义。 Tdikrnl.h 标头文件中定义的前面注册和回调函数。 这些标头文件是在 Microsoft Windows 驱动程序开发工具包 (DDK) 和 Windows Driver Kit (WDK) 中可用。 有关 TDI Plug and Play (PnP) 通知的详细信息，请参阅[TDI 客户端回调](https://msdn.microsoft.com/library/windows/hardware/ff565081)并[TDI 客户端事件和即插即用通知处理程序](https://msdn.microsoft.com/library/windows/hardware/ff565082)。

在系统启动时 TDI 调用代理驱动程序的地址添加回调，以指示当前处于活动状态的所有 IP 地址。 TDI 每当 TCP/IP 传输协议向 TDI 注册新的 IP 地址也会调用此回调。 代理驱动程序包括在其列表中的 IP 地址分配给代理驱动程序的 Nic 这些地址。 驱动程序的地址添加回调应及时地返回控件，如果驱动程序无法识别在 NIC *DeviceName*。

每当向 TDI 指示 TCP/IP 传输协议，已删除 NIC，TDI 调用代理驱动程序的地址删除回调。 如果 NIC 的 IP 地址属于其中一个代理驱动程序的 Nic，代理驱动程序从列表中删除 IP 地址。

**请注意**  TDI 将不支持在 Microsoft Windows 版本在 Windows Vista 后。 使用[Windows 筛选平台](https://msdn.microsoft.com/library/windows/hardware/ff571067)或[Winsock 内核](https://msdn.microsoft.com/library/windows/hardware/ff571083)相反。

 

 

 





