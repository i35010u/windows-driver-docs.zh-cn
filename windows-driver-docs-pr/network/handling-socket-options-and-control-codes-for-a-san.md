---
title: 处理 SAN 的套接字选项和控制代码
description: 处理 SAN 的套接字选项和控制代码
ms.assetid: 5c07d0e3-b6d7-4daf-8b3f-80aafd7c7a37
keywords:
- Windows 套接字直接 WDK SAN 套接字选项
- SAN 套接字 WDK，选项
- 检索 SAN 套接字选项
- SAN 服务提供商 WDK，状态信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad1c3ab12f6229eb16637e4e770484feae08f8d8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561738"
---
# <a name="handling-socket-options-and-control-codes-for-a-san"></a>处理 SAN 的套接字选项和控制代码





Windows 套接字开关，结合 TCP/IP 提供程序，处理最**WSPGetSockOpt**， **WSPSetSockOpt**，并**WSPIoctl**由应用程序发出的呼叫。 这些请求通常是用于设置和检索选项和与应用程序的套接字关联的操作参数。 交换机通常不转发到 SAN 服务提供程序除外所述在以下各节中的这些调用。

### <a name="retrieving-san-socket-options"></a>检索 SAN 套接字选项

Windows 套接字开关调用 SAN 服务提供商[ **WSPGetSockOpt** ](https://msdn.microsoft.com/library/windows/hardware/ff566292)函数并传递以下的套接字选项，以检索该选项的当前值之一，如果 SAN 服务提供程序支持该选项：

<a href="" id="so-debug"></a>因此\_调试  
SAN 服务提供程序不需要支持此选项。 它们是建议，但不是要求提供输出调试信息，如果应用程序设置等\_调试选项。

<a href="" id="so-max-msg-size"></a>SO\_MAX\_MSG\_SIZE  
SAN 服务提供程序必须支持此选项，如果基础 SAN 传输是面向消息的传输限制开关可以在 SAN 服务提供商的调用中发送的数据量[ **WSPSend**](https://msdn.microsoft.com/library/windows/hardware/ff566316)函数。 此开关不随后将发送请求传递到超过 SAN 服务提供程序返回的此选项的值的大小的 SAN 服务提供程序。

<a href="" id="so-max-rdma-size"></a>SO\_MAX\_RDMA\_SIZE  
如果基础 SAN 传输的限制开关可以传输中的数据量调用为 SAN 服务提供商的 SAN 服务提供程序必须支持此选项[ **WSPRdmaRead** ](https://msdn.microsoft.com/library/windows/hardware/ff566304)或[**WSPRdmaWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff566306)函数。 此开关不会随后 RDMA 传输向传递请求超过 SAN 服务提供程序返回的此选项的值的大小的 SAN 服务提供程序。

<a href="" id="so-rdma-threshold-size"></a>因此\_RDMA\_阈值\_大小  
SAN 服务提供程序支持此选项可指示其首选项的最小开关可以传输到任一 SAN 服务提供程序的调用中的数据量**WSPRdmaRead**或**WSPRdmaWrite**函数。 但是，可以切换设置实际的阈值的值不同于 SAN 服务提供程序返回的值。 随后调用开关**WSPRdmaRead**或**WSPRdmaWrite**函数来传输数据块 （RDMA 传输），超过此阈值的大小和**WSPSend**或**WSPRecv**函数将是小于或等于此阈值大小的数据块 （面向消息的传输）。

<a href="" id="so-group-id--so-group-priority"></a>因此\_组\_ID，因此\_组\_优先级  
如果它支持的服务质量 (QoS)，SAN 服务提供程序必须支持这些选项。 否则，交换机将这些选项转发到 TCP/IP 提供程序，用于维护默认值。 SAN 服务提供程序指示它通过设置 XP1 支持 QoS\_QOS\_中的受支持位**dwServiceFlags** WSAPROTOCOL 成员\_信息结构。

### <a name="setting-san-socket-options"></a>设置套接字选项的 SAN

Windows 套接字开关调用 SAN 服务提供商[ **WSPSetSockOpt** ](https://msdn.microsoft.com/library/windows/hardware/ff566318)函数并传递以下的套接字选项，若要设置该选项的值之一，如果 SAN 服务提供程序支持选项：

<a href="" id="so-debug"></a>因此\_调试  
此套接字选项的说明，请参阅前面的列表。

<a href="" id="so-group-priority"></a>因此\_组\_优先级  
此套接字选项的说明，请参阅前面的列表。

### <a name="accessing-san-socket-information"></a>访问 SAN 套接字信息

Windows 套接字开关调用 SAN 服务提供商[ **WSPIoctl** ](https://msdn.microsoft.com/library/windows/hardware/ff566296)函数并传递以下控件之一代码来设置或检索该 SAN 服务提供程序信息，如果 SAN服务提供程序支持该控件的代码：

<a href="" id="sio-get-extension-function-pointer"></a>SIO\_获取\_扩展\_函数\_指针  
检索指向 SAN 服务提供程序必须支持扩展函数的指针。 有关扩展函数详细信息，请参阅[Windows 套接字的 SPI 扩展 San](windows-sockets-spi-extensions-for-sans.md)。 输入的缓冲区**WSPIoctl**调用包含其值确定指定的扩展函数的 GUID。 SAN 服务提供程序中请求的函数返回指向**WSPIoctl**的输出缓冲区。 下表包含 Guid 为 SAN 服务提供程序可以支持扩展函数：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">扩展函数</th>
<th align="left">GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566311" data-raw-source="[&lt;strong&gt;WSPRegisterMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566311)"><strong>WSPRegisterMemory</strong></a></p></td>
<td align="left"><p>{C0B422F5-F58C-11d1-AD6C-00C04FA34A2D}</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566279" data-raw-source="[&lt;strong&gt;WSPDeregisterMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566279)"><strong>WSPDeregisterMemory</strong></a></p></td>
<td align="left"><p>{C0B422F6-F58C-11d1-AD6C-00C04FA34A2D}</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566313" data-raw-source="[&lt;strong&gt;WSPRegisterRdmaMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566313)"><strong>WSPRegisterRdmaMemory</strong></a></p></td>
<td align="left"><p>{C0B422F7-F58C-11d1-AD6C-00C04FA34A2D}</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566281" data-raw-source="[&lt;strong&gt;WSPDeregisterRdmaMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566281)"><strong>WSPDeregisterRdmaMemory</strong></a></p></td>
<td align="left"><p>{C0B422F8-F58C-11d1-AD6C-00C04FA34A2D}</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566306" data-raw-source="[&lt;strong&gt;WSPRdmaWrite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566306)"><strong>WSPRdmaWrite</strong></a></p></td>
<td align="left"><p>{C0B422F9-F58C-11d1-AD6C-00C04FA34A2D}</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566304" data-raw-source="[&lt;strong&gt;WSPRdmaRead&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566304)"><strong>WSPRdmaRead</strong></a></p></td>
<td align="left"><p>{C0B422FA-F58C-11d1-AD6C-00C04FA34A2D}</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566299" data-raw-source="[&lt;strong&gt;WSPMemoryRegistrationCacheCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566299)"><strong>WSPMemoryRegistrationCacheCallback</strong></a></p></td>
<td align="left"><p>{E5DA4AF8-D824-48CD-A799-6337A98ED2AF}</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="sio-get-qos--sio-get-group-qos--sio-set-qos--sio-set-group-qos"></a>SIO\_GET\_QOS, SIO\_GET\_GROUP\_QOS, SIO\_SET\_QOS, SIO\_SET\_GROUP\_QOS  
如果它支持 QoS，SAN 服务提供程序必须支持这些控制代码。 否则，交换机将这些选项转发到 TCP/IP 提供程序，用于维护默认值。 一个提供程序指示它通过设置 XP1 支持 QoS\_QOS\_中的受支持位**dwServiceFlags** WSAPROTOCOL 成员\_信息结构。

<a href="" id="sio-address-list-query"></a>SIO\_地址\_列表\_查询  
检索分配给网络接口卡 (Nic) SAN 服务提供程序控件的本地 IP 地址的列表。 SAN 服务提供商使用套接字\_地址\_定义，如下所示，若要返回的列表中的列表结构**WSPIoctl**的输出缓冲区：

```C++
typedef struct _SOCKET_ADDRESS_LIST {
    INT             iAddressCount; 
    SOCKET_ADDRESS  Address[1]; 
} SOCKET_ADDRESS_LIST, FAR * LPSOCKET_ADDRESS_LIST;
```

此结构的成员包含下列信息：

<a href="" id="iaddresscount"></a>**iAddressCount**  
在列表中指定地址结构的数。

<a href="" id="address"></a>**地址**  
IP 地址结构的数组。

此开关在内部使用此 IOCTL 代码来决定是否使用给定的 SAN 服务提供程序来执行应用程序的请求进行连接，或以侦听传入连接。 开关将实际的应用程序的本地 IP 地址列表的请求转发到 TCP/IP 提供程序。 切换还使用 TCP/IP 提供程序来检测所有 SAN 都服务提供程序都服务的地址列表中的更改。 TCP/IP 的更改进行报告后，此开关会查询所有 SAN 服务提供程序刷新其列表。

 

 





