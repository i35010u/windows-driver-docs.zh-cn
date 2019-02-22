---
title: 虚拟工作站
description: 虚拟工作站
ms.assetid: 6228439c-4c01-4fa9-8b45-b46ed90fa661
keywords:
- 虚拟工作站 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91677b2477e326808e179bbd02c8d702153036a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533260"
---
# <a name="virtual-station"></a>虚拟工作站




 

操作系统从 NDIS 6.20 (Windows 7) 开始，提供虚拟工作站 (VSTA) 可 802.11 微型端口驱动程序与之交互。

独立硬件供应商 (IHV) 使用 VSTA 功能通过[IHV 可扩展性框架](overview-of-ihv-extensibility.md)而非通过 Win32 应用程序编程接口 (Api)。

当 IHV 扩展 DLL 调用启动的虚拟工作站创建[ **Dot11ExtRequestVirtualStation** ](https://msdn.microsoft.com/library/windows/hardware/ff547556)函数。 操作系统会创建只有一个虚拟工作站的计算机上在次，且仅当 IHV 扩展 DLL 颁发**Dot11ExtRequestVirtualStation**请求。

操作系统调用[ *Dot11ExtIhvInitVirtualStation* ](https://msdn.microsoft.com/library/windows/hardware/ff547475)函数以初始化虚拟工作站操作 IHV 扩展 DLL。 此调用还可以初始化操作系统和 DLL 之间的用户模式 API 接口。

**请注意**  若要确保以一致的方式创建的虚拟工作站，计算机应具有只能安装一个 IHV 扩展 DLL，尝试使用虚拟工作站的功能。 即使安装多个 DLL，则可以创建只有一个虚拟工作站。 操作系统不能保证该 DLL 将有权访问虚拟工作站后重新启动计算机。 请注意，如果已具有已在一个 DLL 和第二个 DLL 的请求时创建的虚拟工作站然后调用**Dot11ExtRequestVirtualStation**，可能会返回成功代码，但将不会创建第二个虚拟工作站。
IHV 扩展 DLL 后，它调用设置两分钟计时器**Dot11ExtRequestVirtualStation**函数。 如果在计时器过期虚拟工作站适配器到达事件之前，应假定 DLL 不创建虚拟工作站。

 

### <a href="" id="extensible-ap-virtual-station-interactions"></a> 可扩展亚太/虚拟工作站交互

如果您的驱动程序实现虚拟工作站功能，但不能承受两[可扩展接入点 (ExtAP)](extensible-access-point-operation-mode.md)和虚拟工作站连接在不同端口上同时，该驱动程序应执行以下操作。

-   告知操作系统用于 ExtAP 的端口是否可以或不能在所有时间维持功能。 具体而言，该驱动程序应发出以下状态的指示 ExtAP 端口上使用相应的状态代码 ( [ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373) - &gt; **StatusCode**) 和原因代码：

    <a href="" id="ndis-status-dot11-stop-ap"></a>[NDIS\_STATUS\_DOT11\_STOP\_AP](https://msdn.microsoft.com/library/windows/hardware/ff567366)  
    指示不能在 ExtAP 端口上持续很 AP 的功能。 在这种情况下，设置[ **DOT11\_停止\_AP\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff548783) - &gt; **ulReason**为的值DOT11\_停止\_AP\_原因\_AP\_活动。 发出此状态指示在以下情况下：

    -   若要使用的共享的资源，同时虚拟工作站和 ExtAP 连接会阻止虚拟工作站端口之前
    -   如果 ExtAP 端口转换到 ExtAP INIT 状态和虚拟工作站资源使用会阻止成功初始化 ExtAP 端口。

    <a href="" id="---------ndis-status-dot11-can-sustain-ap"></a>[NDIS\_状态\_DOT11\_可以\_SUSTAIN\_亚太](https://msdn.microsoft.com/library/windows/hardware/ff567323)  
    指示虚拟工作站端口已断开连接，或该使用的虚拟工作站资源将不会阻止该端口的成功转换到 ExtAP INIT 状态。

-   在连接到虚拟工作站端口时，调用[ **Dot11ExtSetVirtualStationAPProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff547609)函数以提供有关托管的虚拟工作站的接入点实现的信息连接。

-   失败的虚拟工作站端口连接，如果 ExtAP 端口在操作状态下运行，并且发生以下情况之一：
    -   一个或多个客户端已 ExtAP 端口上运行。
    -   尝试启动复制的连接的虚拟工作站[托管的无线网络](https://go.microsoft.com/fwlink/p/?linkid=152328)设置。

### <a href="" id="native-802-11-ihv-extensibility-functions-that-support-a-virtual-stati"></a> 本机 802.11 IHV 扩展函数支持虚拟工作站

[**Dot11ExtQueryVirtualStationProperties**](https://msdn.microsoft.com/library/windows/hardware/ff547544)

[**Dot11ExtReleaseVirtualStation**](https://msdn.microsoft.com/library/windows/hardware/ff547549)

[**Dot11ExtRequestVirtualStation**](https://msdn.microsoft.com/library/windows/hardware/ff547556)

[**Dot11ExtSetVirtualStationAPProperties**](https://msdn.microsoft.com/library/windows/hardware/ff547609)

### <a href="" id="structures-that-support-a-virtual-station"></a> 支持虚拟工作站的结构

[**DOT11EXT\_VIRTUAL\_STATION\_AP\_PROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff547641)

[**DOT11EXT\_VIRTUAL\_STATION\_APIS**](https://msdn.microsoft.com/library/windows/hardware/ff547639)

 

 





