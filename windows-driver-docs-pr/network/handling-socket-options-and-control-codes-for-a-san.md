---
title: 处理 SAN 的套接字选项和控制代码
description: 处理 SAN 的套接字选项和控制代码
ms.assetid: 5c07d0e3-b6d7-4daf-8b3f-80aafd7c7a37
keywords:
- Windows 套接字直接 WDK，SAN 套接字选项
- SAN 套接字 WDK，选项
- 检索 SAN 套接字选项
- SAN 服务提供商 WDK，状态信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42c837461b25f623a0c78cccad250d47221ba8e1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211087"
---
# <a name="handling-socket-options-and-control-codes-for-a-san"></a>处理 SAN 的套接字选项和控制代码





Windows 套接字交换机与 TCP/IP 提供程序一起处理由应用程序启动的大多数 **WSPGetSockOpt**、 **WSPSetSockOpt**和 **WSPIoctl** 调用。 这些请求通常用于设置和检索与应用程序的套接字关联的选项和操作参数。 通常，此开关不会将这些调用转发到 SAN 服务提供程序，如以下部分中所述。

### <a name="retrieving-san-socket-options"></a>检索 SAN 套接字选项

如果 SAN 服务提供程序支持该选项，Windows 套接交换机将调用 SAN 服务提供程序的 [**WSPGetSockOpt**](/previous-versions/windows/hardware/network/ff566292(v=vs.85)) 函数，并传递以下套接字选项之一来检索该选项的当前值：

<a href="" id="so-debug"></a>SO \_ 调试  
SAN 服务提供程序不需要支持此选项。 如果应用程序设置了 SO 调试选项，则建议（但不要求）提供输出调试信息 \_ 。

<a href="" id="so-max-msg-size"></a>\_最大 \_ 消息 \_ 大小  
如果基础 SAN 传输面向消息，且传输限制了交换机在对 SAN 服务提供程序的 [**WSPSend**](/previous-versions/windows/hardware/network/ff566316(v=vs.85)) 函数的调用中可以发送的数据量，则 SAN 服务提供程序必须支持此选项。 然后，此开关不会将发送请求传递到超过 SAN 服务提供程序为此选项的值返回的大小的 SAN 服务提供程序。

<a href="" id="so-max-rdma-size"></a>\_最大 \_ RDMA \_ 大小  
如果基础 SAN 传输限制了交换机在调用 SAN 服务提供程序的 [**WSPRdmaRead**](/previous-versions/windows/hardware/network/ff566304(v=vs.85)) 或 [**WSPRdmaWrite**](/previous-versions/windows/hardware/network/ff566306(v=vs.85)) 函数时可以传输的数据量，则 san 服务提供程序必须支持此选项。 然后，此开关不会将 RDMA 传输请求传递到 SAN 服务提供程序，超过了此选项的值所返回的 SAN 服务提供程序的大小。

<a href="" id="so-rdma-threshold-size"></a>SO \_ RDMA \_ 阈值 \_ 大小  
SAN 服务提供程序支持此选项，以便在对 SAN 服务提供程序的 **WSPRdmaRead** 或 **WSPRdmaWrite** 函数的调用中，为交换机可以传输的最小数据量指示其首选项。 但是，该开关可以将实际阈值设置为与 SAN 服务提供程序返回的值不同的值。 此开关随后将调用 **WSPRdmaRead** 或 **WSPRdmaWrite** 函数以传输数据块 (RDMA 传输超过此阈值大小的) ，并调用 **WSPSend** 或 **WSPRecv** 函数将数据块传输 (小于或等于此阈值大小的面向消息的) 传输。

<a href="" id="so-group-id--so-group-priority"></a>这样，组 ID 就会成为 \_ \_ \_ 组 \_ 优先级  
如果 SAN 服务提供程序支持服务质量 (QoS) ，则该提供程序必须支持这些选项。 否则，开关会将这些选项转发到 TCP/IP 提供程序，后者维护默认值。 SAN 服务提供程序通过 \_ \_ 在 WSAPROTOCOL INFO 结构的 **dwServiceFlags** 成员中设置 XP1 QoS 支持的位来指示它支持 QoS \_ 。

### <a name="setting-san-socket-options"></a>设置 SAN 套接字选项

如果 SAN 服务提供程序支持该选项，Windows 套接字交换机将调用 SAN 服务提供程序的 [**WSPSetSockOpt**](/previous-versions/windows/hardware/network/ff566318(v=vs.85)) 函数，并传递以下套接字选项之一来设置该选项的值：

<a href="" id="so-debug"></a>SO \_ 调试  
有关此套接字选项的说明，请参阅前面的列表。

<a href="" id="so-group-priority"></a>SO \_ 组 \_ 优先级  
有关此套接字选项的说明，请参阅前面的列表。

### <a name="accessing-san-socket-information"></a>访问 SAN 套接字信息

如果 SAN 服务提供程序支持该控制代码，Windows 套接字交换机会调用 SAN 服务提供程序的 [**WSPIoctl**](/previous-versions/windows/hardware/network/ff566296(v=vs.85)) 函数，并传递以下控制代码之一来设置或检索该 san 服务提供程序的信息：

<a href="" id="sio-get-extension-function-pointer"></a>SIO \_ GET \_ EXTENSION \_ 函数 \_ 指针  
检索指向 SAN 服务提供程序必须支持的扩展函数的指针。 有关扩展函数的详细信息，请参阅 [适用于 san 的 Windows 套接字 SPI 扩展](windows-sockets-spi-extensions-for-sans.md)。 **WSPIoctl**调用的输入缓冲区包含其值标识指定扩展函数的 GUID。 SAN 服务提供程序将指针返回到 **WSPIoctl**的输出缓冲区中请求的函数。 下表包含 SAN 服务提供商可以支持的扩展函数的 Guid：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Extension 函数</th>
<th align="left">GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566311(v=vs.85)" data-raw-source="[&lt;strong&gt;WSPRegisterMemory&lt;/strong&gt;](/previous-versions/windows/hardware/network/ff566311(v=vs.85))"><strong>WSPRegisterMemory</strong></a></p></td>
<td align="left"><p>{C0B422F5-F58C-11d1-AD6C-00C04FA34A2D}</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566279(v=vs.85)" data-raw-source="[&lt;strong&gt;WSPDeregisterMemory&lt;/strong&gt;](/previous-versions/windows/hardware/network/ff566279(v=vs.85))"><strong>WSPDeregisterMemory</strong></a></p></td>
<td align="left"><p>{C0B422F6-F58C-11d1-AD6C-00C04FA34A2D}</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566313(v=vs.85)" data-raw-source="[&lt;strong&gt;WSPRegisterRdmaMemory&lt;/strong&gt;](/previous-versions/windows/hardware/network/ff566313(v=vs.85))"><strong>WSPRegisterRdmaMemory</strong></a></p></td>
<td align="left"><p>{C0B422F7-F58C-11d1-AD6C-00C04FA34A2D}</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566281(v=vs.85)" data-raw-source="[&lt;strong&gt;WSPDeregisterRdmaMemory&lt;/strong&gt;](/previous-versions/windows/hardware/network/ff566281(v=vs.85))"><strong>WSPDeregisterRdmaMemory</strong></a></p></td>
<td align="left"><p>{C0B422F8-F58C-11d1-AD6C-00C04FA34A2D}</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566306(v=vs.85)" data-raw-source="[&lt;strong&gt;WSPRdmaWrite&lt;/strong&gt;](/previous-versions/windows/hardware/network/ff566306(v=vs.85))"><strong>WSPRdmaWrite</strong></a></p></td>
<td align="left"><p>{C0B422F9-F58C-11d1-AD6C-00C04FA34A2D}</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566304(v=vs.85)" data-raw-source="[&lt;strong&gt;WSPRdmaRead&lt;/strong&gt;](/previous-versions/windows/hardware/network/ff566304(v=vs.85))"><strong>WSPRdmaRead</strong></a></p></td>
<td align="left"><p>{C0B422FA-F58C-11d1-AD6C-00C04FA34A2D}</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566299(v=vs.85)" data-raw-source="[&lt;strong&gt;WSPMemoryRegistrationCacheCallback&lt;/strong&gt;](/previous-versions/windows/hardware/network/ff566299(v=vs.85))"><strong>WSPMemoryRegistrationCacheCallback</strong></a></p></td>
<td align="left"><p>{E5DA4AF8-D824-48CD-A799-6337A98ED2AF}</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="sio-get-qos--sio-get-group-qos--sio-set-qos--sio-set-group-qos"></a>SIO \_ 获取 \_ QOS，SIO \_ 获取 \_ 组 \_ QOS，SIO \_ 集 \_ QOS，SIO \_ 设置 \_ 组 \_ QOS  
如果 SAN 服务提供程序支持 QoS，则该提供程序必须支持这些控制代码。 否则，开关会将这些选项转发到 TCP/IP 提供程序，后者维护默认值。 提供程序指示它通过 \_ \_ 在 WSAPROTOCOL INFO 结构的 **dwServiceFlags** 成员中设置 XP1 qos 支持的位来支持 QoS \_ 。

<a href="" id="sio-address-list-query"></a>SIO \_ 地址 \_ 列表 \_ 查询  
检索分配给网络接口卡的本地 IP 地址列表，这些地址 (Nic 服务提供程序控制的 Nic) 。 SAN 服务提供程序使用 \_ 如下所示的套接字地址 \_ 列表结构来返回 **WSPIoctl**的输出缓冲区中的列表：

```C++
typedef struct _SOCKET_ADDRESS_LIST {
    INT             iAddressCount; 
    SOCKET_ADDRESS  Address[1]; 
} SOCKET_ADDRESS_LIST, FAR * LPSOCKET_ADDRESS_LIST;
```

此结构的成员包含以下信息：

<a href="" id="iaddresscount"></a>**iAddressCount**  
指定列表中的地址结构数。

<a href="" id="address"></a>**地址**  
IP 地址结构的数组。

开关在内部使用此 IOCTL 代码来确定是否使用给定的 SAN 服务提供程序来执行应用程序的请求，以建立连接或侦听传入连接。 开关将本地 IP 地址列表的实际应用程序请求转发给 TCP/IP 提供程序。 开关还使用 TCP/IP 提供程序来检测所有 SAN 服务提供程序服务的地址列表中的更改。 TCP/IP 报告更改后，交换机会查询所有 SAN 服务提供商以刷新其列表。

 

