---
title: 关联前的操作概述
description: 关联前的操作概述
ms.assetid: c33cf228-720f-4204-820c-0fb9a288bc6e
keywords:
- 预关联操作 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c06e828d6712816d98a2bb20c1cb4a1f9d0baeac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355224"
---
# <a name="pre-association-operation-overview"></a>关联前的操作概述




 

用户已经选择了基本的服务设置 (BSS) 网络连接的配置文件后，操作系统将调用[ *Dot11ExtIhvPerformPreAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547499)函数启动预关联操作。 当调用此函数时，IHV 扩展 DLL 执行以下任务：

-   验证连接和安全配置文件的 IHV 定义扩展。

    如果 IHV 扩展 DLL 确定配置文件不正确，则返回相应的错误代码，如在 Winerror.h 中定义。 在此情况下，操作系统会通知用户不能使用网络配置文件。

-   启动基于连接和安全配置文件的 IHV 定义扩展预关联操作。

    预关联操作启动后，就必须完成异步调用[ *Dot11ExtIhvPerformPreAssociate*](https://msdn.microsoft.com/library/windows/hardware/ff547499)。

IHV 扩展 DLL 完成预关联操作通过调用[ **Dot11ExtPreAssociateCompletion**](https://msdn.microsoft.com/library/windows/hardware/ff547538)。 在此调用，操作系统将启动连接操作通过发出的集请求[OID\_DOT11\_CONNECT\_请求](https://msdn.microsoft.com/library/windows/hardware/ff569122)到本机 802.11 微型端口驱动程序，用于管理将 WLAN 适配器。

下图显示涉及预关联操作过程的步骤。

![说明预关联操作过程中所涉及的步骤的关系图](images/ihv-ext-preassoc.png)

当[ *Dot11ExtIhvPerformPreAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547499)调用时，连接性和安全性的 IHV 定义扩展通过以下参数配置文件的操作系统阶段。

<a href="" id="pihvprofileparams"></a>*pIhvProfileParams*  
此参数传递一个指向[ **DOT11EXT\_IHV\_配置文件\_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff547630)结构，它指定属性的基本服务设置 (BSS)要应用的网络配置文件的网络。 例如， **DOT11EXT\_IHV\_配置文件\_PARAMS**结构指定的服务集标识符 (SSID) 和 BSS 网络的类型。

<a href="" id="pihvconnprofile"></a>*pIhvConnProfile*  
此参数传递一个指向[ **DOT11EXT\_IHV\_连接\_配置文件**](https://msdn.microsoft.com/library/windows/hardware/ff547619)结构，其中包含连接配置文件的设置。 操作系统仅连接配置文件由 IHV 定义并由用户选择传递扩展插件。

<a href="" id="pihvsecprofile"></a>*pIhvSecProfile*  
此参数传递一个指向[ **DOT11EXT\_IHV\_安全\_配置文件**](https://msdn.microsoft.com/library/windows/hardware/ff547632)结构，其中包含的安全配置文件的设置。 操作系统仅传递到由 IHV 定义并由用户选择的安全配置文件的扩展。

<a href="" id="pconnectablebssid"></a>*pConnectableBssid*  
此参数传递一个指向[ **DOT11\_BSS\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff547668)结构，其中包含一个或多个 802.11 信号或探测响应帧，该服务设置标识符 （SSID) 的 BSS 网络使用的 DLL 将执行预关联操作。

执行预关联操作时，IHV 扩展 DLL 可以执行以下操作：

-   调用[ **Dot11ExtNicSpecificExtension** ](https://msdn.microsoft.com/library/windows/hardware/ff547526)函数专有的配置的发出请求的网络连接到本机 802.11 微型端口驱动程序。

    通过*pIhvConnProfile*并*pIhvProfileParams*参数，IHV 扩展 DLL 可以确定用户已选择的专有连接设置。

    通过*pConnectableBssid*参数，IHV 扩展 DLL 可以确定的属性 BSS 网络以及可以配置专用网络设置相应地。

-   配置用于通过 BSS 网络连接的专有身份验证和密码的算法将 WLAN 适配器。

    通过*pszXmlFragmentIhvSecurity*参数，IHV 扩展 DLL 可以确定由用户选择可使用专用安全的算法。

    若要设置的安全算法，可以调用以下 IHV 扩展性函数。

    -   [**Dot11ExtSetAuthAlgorithm**](https://msdn.microsoft.com/library/windows/hardware/ff547571)
    -   [**Dot11ExtSetUnicastCipherAlgorithm**](https://msdn.microsoft.com/library/windows/hardware/ff547606)
    -   [**Dot11ExtSetMulticastCipherAlgorithm**](https://msdn.microsoft.com/library/windows/hardware/ff547599)
-   调用[ **Dot11ExtSendUIRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff547567)函数请求 IHV UI 扩展 DLL 提示用户输入安全参数，例如用户的凭据。

-   调用[ **Dot11ExtSetEtherTypeHandling** ](https://msdn.microsoft.com/library/windows/hardware/ff547587)函数以注册该 DLL 会收到安全数据包 IEEE EtherTypes 的列表。 注册列表后，操作系统将调用[ *Dot11ExtIhvReceivePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff547513)其 EtherType 与列表中的某个条目匹配的每个数据包的 IHV 处理程序函数。

    IHV 扩展 DLL 还可以指定将从有效负载解密中排除的 EtherTypes 的列表。 有关注册 EtherTypes 的详细信息，请参阅[IEEE EtherType 处理](ieee-ethertype-handling.md)。

-   调用[ **Dot11ExtSetProfileCustomUserData** ](https://msdn.microsoft.com/library/windows/hardware/ff547603)函数是特定于用户和当前 BSS 网络配置文件在注册表中保存数据。

-   调用[ **Dot11ExtGetProfileCustomUserData** ](https://msdn.microsoft.com/library/windows/hardware/ff547430)函数以从特定于用户和当前 BSS 网络配置文件的注册表中检索数据。

有关 IHV 扩展性函数的详细信息，请参阅[本机 802.11 IHV 扩展性函数](https://msdn.microsoft.com/library/windows/hardware/ff560609)。

连接操作的 BSS 网络的详细信息，请参阅[连接操作](connection-operations.md)。

 

 





