---
title: 本机 802.11 IHV 扩展 DLL 概述
description: 本机 802.11 IHV 扩展 DLL 概述
ms.assetid: 6a3d3e62-41b3-4ae2-a379-273431a36bb1
keywords:
- IHV 扩展 DLL WDK 本机802.11，关于本机 802.11 IHV 扩展 DLL
- 本机 802.11 IHV 扩展 DLL WDK，关于本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 046c62e2400a2e7f753b5f360c90f0bc25c9d6dc
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217038"
---
# <a name="native-80211-ihv-extensions-dll-overview"></a>本机 802.11 IHV 扩展 DLL 概述




 

通过 IHV 扩展 DLL，独立硬件供应商 (IHV) 可以支持以下各项：

-   专用或非标准身份验证算法。 通过此支持，IHV 扩展 DLL 发送并接收与身份验证算法相关的所有安全数据包。

    IHV 扩展 DLL 还可以支持操作系统不支持的网络配置的标准身份验证算法。 例如，DLL 可支持具有预共享密钥的 Wi-fi 受保护的访问， (在) 身份验证算法 (IBSS) 网络，这是 Windows Vista 不支持的配置。

-   专用或非标准密码算法。 通过此支持，IHV 扩展 DLL 负责派生密码密钥并将密钥下载到本机802.11 微型端口驱动程序。

    IHV 扩展 DLL 还可以支持操作系统不支持的网络配置的标准密码算法。 例如，DLL 可支持 (TKIP) over IBSS 网络（Windows Vista 不支持的配置）的临时密钥完整性协议。

-   验证网络配置文件的专有扩展。 例如，IHV 扩展 DLL 负责验证由 IHV 定义的安全选项的用户设置。

-   本机802.11 微型端口驱动程序的配置。 例如，在使用微型端口驱动程序开始连接操作之前，操作系统将调用 [*Dot11ExtIhvPerformPreAssociate*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate) 函数，以便 IHV 扩展 DLL 可以使用与 BSS 网络连接相关的专有扩展来配置驱动程序。

-   IHV UI 扩展 DLL 的接口。 通过此接口，IHV 扩展 DLL 可以请求用户输入或通知。 有关 IHV UI 扩展 DLL 的详细信息，请参阅 [本机 802.11 IHV Ui 扩展 dll](native-802-11-ihv-ui-extensions-dll2.md)。

本机 802.11 IHV 扩展性主机进程在第一次到达时将 IHV 扩展 DLL 加载到其进程空间，并检测到安装了 DLL 的无线 LAN (WLAN) 适配器。 有关本机 802.11 IHV 扩展性主机进程和本机802.11 框架的详细信息，请参阅 [本机802.11 软件体系结构](/previous-versions/windows/hardware/wireless/native-802-11-software-architecture)。

本机 802.11 IHV 扩展性主机进程通过其 IHV 扩展性功能提供 API。 通过此 API，IHV 扩展 DLL 可以对本机802.11 微型端口驱动程序或 IHV UI 扩展 DLL 进行接口。 有关 IHV 扩展性函数的详细信息，请参阅 [本机 802.11 IHV 扩展性函数](./native-802-11-ihv-extensibility-functions.md)。

同样，IHV 扩展 DLL 通过其 IHV 处理函数提供 API。 本机 802.11 IHV 扩展性主机进程将此 API 用于各种操作，如启动预关联或后关联操作。 有关 IHV 处理程序函数的详细信息，请参阅 [本机 802.11 IHV 处理程序函数](./native-802-11-ihv-handler-functions.md)。

 

 