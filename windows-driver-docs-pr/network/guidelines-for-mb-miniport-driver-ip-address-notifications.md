---
title: 有关 MB 微型端口驱动程序 IP 地址通知的指导原则
description: 有关 MB 微型端口驱动程序 IP 地址通知的指导原则
ms.assetid: 23d74bc4-5648-45e3-a603-350d71bb16e3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbf70c2ecb3338ee39a93b905e4c52a1f8975cd1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349825"
---
# <a name="guidelines-for-mb-miniport-driver-ip-address-notifications"></a>有关 MB 微型端口驱动程序 IP 地址通知的指导原则


指定的 MB 微型端口驱动程序*EnableDhcp*等于零，其 INF 文件中可以使用[IP 帮助程序](ip-helper.md)和关联[函数](https://msdn.microsoft.com/library/windows/hardware/ff557018)在内核模式下创建、 更改，并删除 IP 地址：

若要在内核模式中使用的 IP 帮助程序函数，微型端口驱动程序必须包括 Netioapi.h 标头文件，并针对 Netio.lib 链接。

微型端口驱动程序时指定*EnableDhcp*等于零它们所需执行以下操作以便通知 MB 服务有关的任何以下事件：

-   设置 MB 接口的 IP 地址

-   设置默认网关地址

-   更新的 DNS 地址

IP 地址和默认网关使用 IP 帮助程序 API 设置保留网络连接或断开连接事件，或兼而有之。 因此，如果新的 IP 地址或默认网关，或两者，值为不同于当前设置的值，微型端口驱动程序应首先在网络连接事件上设置新值之前清除以前的值。

**请注意**  微型端口驱动程序可以找到**LUID**并**索引**MB 接口中的**NetLuid**或**IfIndex**的成员[ **NDIS\_微型端口\_INIT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff565972)传递给微型端口驱动程序的结构[*MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数。

 

### <a name="resetting-the-ip-address-and-gateway-address"></a>重置的 IP 地址和网关地址

TCP/IP 堆栈，如必需的筛选器驱动程序，加载某些更改可以删除由 IP 帮助程序函数设置的 IP 和网关地址。 如果对 TCP/IP 堆栈的更改删除设置，微型端口驱动程序必须重置的 IP 和网关地址。

微型端口驱动程序应使用以下过程地址被删除，而必须再次重置时收到通知。

1.  期间**驱动程序初始化**，微型端口驱动程序应指定一个回调函数来注册使用的 IP 接口更改通知[ **NotifyIpInterfaceChange** ](https://msdn.microsoft.com/library/windows/hardware/ff568805). Windows 将调用函数 wheneven 添加、 删除或更改了 IP 接口。

2.  期间**适配器初始化**，微型端口驱动程序应将保存在微型端口驱动程序的本地适配器上下文**LUID**值从[ **NDIS\_微型端口\_INIT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff565972)传递给微型端口驱动程序的结构[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数。 包含的值*NetLuid*用于标识通知回调中使用的适配器的接口。

3.  在中**通知回调**，Windows 将以下参数传递到与注册的通知函数[ **NotifyIpInterfaceChange**](https://msdn.microsoft.com/library/windows/hardware/ff568805):

    -   一个指向[ **MIB\_IPINTERFACE\_行**](https://msdn.microsoft.com/library/windows/hardware/ff559254)结构，其中包含*NetLuid*的微型端口适配器的接口。
    -   通知，可以是类型**MibAddInstance**， **MibDeleteInstance**或**MibParameterNotification**。

    适配器处于连接状态和通知类型时，微型端口驱动程序应重置的 IP 和网关地址**MibAddInstance**，并*NetLuid*中[ **MIB\_IPINTERFACE\_行**](https://msdn.microsoft.com/library/windows/hardware/ff559254)对应于一个微型端口驱动程序的适配器，适配器初始化过程已保存。

    然后，微型端口驱动程序应遵循设置 MB 的接口和设置默认网关地址过程要重置相应的地址的 IP 地址。

4.  期间**驱动程序卸载**，微型端口驱动程序应取消注册通知回调函数使用[ **CancelMibChangeNotify2** ](https://msdn.microsoft.com/library/windows/hardware/ff544864) IP 帮助程序函数。

### <a name="setting-the-ip-address-for-the-mb-interface"></a>设置 MB 接口的 IP 地址

若要设置的 IPv4 地址，请使用以下过程。 可以使用类似的 IP 帮助程序功能设置 IPv6 地址。

1.  使用[ **GetUnicastIpAddressTable** ](https://msdn.microsoft.com/library/windows/hardware/ff552594) IP 帮助程序函数来查找所有 IP 地址的条目在系统中。

2.  对于每个条目的**InterfaceLuid**值匹配**InterfaceLuid** MB 接口的：
    1.  查找匹配上一个连接中使用的 IP 地址的 IP 地址条目。 第一次连接将不具有以前的 IP 地址。
    2.  如果新的 IP 地址不同于以前的 IP 地址，请使用删除上一个连接 IP 地址的 IP 地址条目[ **DeleteUnicastIpAddressEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff546370) IP 帮助程序函数。
    3.  如果新的 IP 地址与以前的 IP 地址相同，请验证所需的项已存在。

3.  如果微型端口驱动程序未在上一循环中找到所需的 IP 地址条目，则应添加新条目。
    1.  使用[ **InitializeUnicastIpAddressEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554886) IP 帮助程序函数来初始化[ **MIB\_UNICASTIPADDRESS\_行**](https://msdn.microsoft.com/library/windows/hardware/ff559308)结构并设置以下结构的成员：
        1.  设置**InterfaceLuid**或**InterfaceIndex**成员，根据需要。
        2.  设置**OnlinePrefixLength**成员。 这是具有一个子网掩码中的值的比特数。 例如，如果子网掩码为 255.255.255.0 **OnlinePrefixLength**应为 24。
        3.  设置**地址**成员。
        4.  设置**PrefixOrigin**成员添加到**IpPrefixOriginManual**。

    2.  传递初始化的 MIB\_UNICASTADDRESS\_到行结构[ **CreateUnicastIpAddressEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff546227) IP 帮助程序函数来创建 IP 地址的条目。

### <a name="setting-default-gateway-address"></a>设置默认网关地址

若要设置的 IPv4 网关地址，请使用以下过程。 可以使用类似的 IP 帮助程序功能来设置 IPv6 网关地址。

1.  使用[ **GetIpForwardTable2** ](https://msdn.microsoft.com/library/windows/hardware/ff552536) IP 帮助程序函数来获取系统中的所有路由条目。

2.  对于每个条目的**InterfaceLuid**值匹配**InterfaceLuid** MB 接口的值的和**DestinationPrefix**是"0.0.0.0/0"，调用[**DeleteIpForwardEntry2** ](https://msdn.microsoft.com/library/windows/hardware/ff546365) IP 帮助程序函数要删除的路由，如果**下一跃点**不等于新网关地址。 否则，路由项已在系统中。

3.  如果微型端口驱动程序未在上一循环中找到所需的路由条目，它应使用添加新条目[ **InitializeIpForwardEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554882) IP 帮助程序函数以初始化[**MIB\_IPFORWARD\_ROW2** ](https://msdn.microsoft.com/library/windows/hardware/ff559245)结构。 初始化结构的以下成员：

    **InterfaceLuid**或**InterfaceIndex** 。

    设置**DestinationPrefix**为 0.0.0.0/0 表示默认网关。 (前缀 0.0.0.0 和 PrefixLength = = 0)

    设置**下一跃点**到默认网关的 IP 地址。

    在初始化期间，其他成员设置为默认值。 微型端口驱动程序应使用这些成员的默认值。

4.  传递[ **MIB\_IPFORWARD\_ROW2** ](https://msdn.microsoft.com/library/windows/hardware/ff559245)结构[ **CreateIpForwardEntry2** ](https://msdn.microsoft.com/library/windows/hardware/ff546209) IP 帮助程序若要设置新的默认网关地址的函数。

### <a name="to-set-dns-addresses"></a>若要设置 DNS 地址

-   设置**名称服务器**注册表项中所述[MB DNS 更新](mb-dns-updates.md)要通知 Windows 的更新的 DNS 地址。

 

 





