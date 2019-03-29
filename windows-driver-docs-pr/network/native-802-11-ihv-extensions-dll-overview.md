---
title: 本机 802.11 IHV 扩展 DLL 概述
description: 本机 802.11 IHV 扩展 DLL 概述
ms.assetid: 6a3d3e62-41b3-4ae2-a379-273431a36bb1
keywords:
- 有关本机 802.11 IHV 扩展 DLL 的 IHV 扩展 DLL WDK 本机 802.11
- 本机 802.11 IHV 扩展 DLL WDK，有关本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba96bc3507d8b2456031985755ce2246157c4fde
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566810"
---
# <a name="native-80211-ihv-extensions-dll-overview"></a>本机 802.11 IHV 扩展 DLL 概述




 

通过非 IHV 扩展 DLL，独立硬件供应商 (IHV) 可以支持以下功能：

-   专有或非标准身份验证算法。 通过这种支持，IHV 扩展 DLL 发送和接收与身份验证算法相关的所有安全数据包。

    IHV 扩展 DLL 还可以用于不受操作系统的网络配置支持标准身份验证算法。 例如，DLL 可支持的 Wi-fi 保护访问，以使用预共享的密钥 (WPA-PSK) 身份验证算法通过独立的基本服务集 (IBSS) 网络，这是 Windows Vista 不支持的配置。

-   专有或非标准密码算法。 通过这种支持，IHV 扩展 DLL 负责派生的加密密钥和下载到本机 802.11 微型端口驱动程序的密钥。

    IHV 扩展 DLL 还可以用于不受操作系统的网络配置支持标准密码算法。 例如，DLL 可支持临时密钥完整性协议 (TKIP) 通过 IBSS 网络，这是 Windows Vista 不支持的配置。

-   网络配置文件的专有扩展的验证。 例如，IHV 扩展 DLL 负责 IHV 定义的安全选项的用户设置的验证。

-   本机 802.11 微型端口驱动程序的配置。 例如，在开始之前连接操作的微型端口驱动程序，操作系统将调用[ *Dot11ExtIhvPerformPreAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547499)函数，以便可以 IHV 扩展 DLL使用与到 BSS 网络连接相关的专有扩展插件配置驱动程序。

-   IHV UI 扩展 DLL 的接口。 通过此接口，IHV 扩展 DLL 可以请求用户输入或通知。 IHV UI 扩展 DLL 的详细信息，请参阅[本机 802.11 IHV UI 扩展 DLL](native-802-11-ihv-ui-extensions-dll2.md)。

本机 802.11 IHV 扩展性主机进程将 IHV 扩展 DLL 加载到在第一个到达和检测为其安装 DLL 的无线 LAN (WLAN) 适配器时的进程空间中。 有关本机 802.11 IHV 扩展性主机进程和本机 802.11 框架的详细信息，请参阅[本机 802.11 软件体系结构](native-802-11-software-architecture.md)。

本机 802.11 IHV 扩展性主机进程提供了一个 API 通过其 IHV 扩展性功能。 通过此 API，IHV 扩展 DLL 可以接口本机 802.11 微型端口驱动程序或 IHV UI 扩展 DLL。 有关 IHV 扩展性函数的详细信息，请参阅[本机 802.11 IHV 扩展性函数](https://msdn.microsoft.com/library/windows/hardware/ff560609)。

同样，IHV 扩展 DLL 提供了通过其 IHV 处理程序函数的 API。 本机 802.11 IHV 扩展性主机进程使用此 API 进行各种操作，例如启动快照前或后关联的操作。 有关 IHV 处理程序函数的详细信息，请参阅[本机 802.11 IHV 处理程序函数](https://msdn.microsoft.com/library/windows/hardware/ff560627)。

 

 





