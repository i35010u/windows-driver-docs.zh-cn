---
title: 发送操作
description: 发送操作
ms.assetid: 84af0abc-c8f2-47d4-b368-7b0216600c95
keywords:
- 发送操作 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b2840ade07e8e9f7531afdc4fe3bf329c1aadae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365761"
---
# <a name="send-operations"></a>发送操作




 

执行后关联操作时，通过调用发起[ *Dot11ExtIhvPerformPostAssociate*](https://msdn.microsoft.com/library/windows/hardware/ff547492)，IHV 扩展 DLL 可以发送通过无线 LAN (WLAN) 适配器的数据包。 有关后关联操作的详细信息，请参阅[后期关联操作](post-association-operations.md)。

通常情况下，该 DLL 安全将数据包发送给数据端口身份验证的访问点 (AP) 使用的算法通过启用[ **Dot11ExtSetAuthAlgorithm**](https://msdn.microsoft.com/library/windows/hardware/ff547571)。 IHV 扩展 DLL 调用**Dot11ExtSetAuthAlgorithm**预关联操作过程中。 有关此操作的详细信息，请参阅[预关联操作](pre-association-operations.md)。

**请注意**  For Windows Vista 中，只有在基础结构的基本服务设置 (BSS) 网络 IHV 扩展 DLL 支持。

 

在发送数据包时，IHV 扩展 DLL 必须遵循这些准则。

-   IHV 扩展 DLL 必须为完整的 802.11 数据数据包，包括 802.11 媒体访问控制 (MAC) 标头、 LLC 封装 （如有必要） 和有效负载数据分配内存。

    下表介绍 IHV 扩展 DLL 或 WLAN 适配器设置的字段和 802.11 MAC 报头中的子字段。

    <table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">字段名称</th>
    <th align="left">子字段名称</th>
    <th align="left">设置的 IHV 扩展 DLL</th>
    <th align="left">由 WLAN 适配器设置</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>Frame 控件</p></td>
    <td align="left"><p>协议版本</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>Frame 控件</p></td>
    <td align="left"><p>在任务栏的搜索框中键入</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>Frame 控件</p></td>
    <td align="left"><p>子类型</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>Frame 控件</p></td>
    <td align="left"><p>到 DS</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>Frame 控件</p></td>
    <td align="left"><p>从 DS</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>Frame 控件</p></td>
    <td align="left"><p>多个片段</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>Frame 控件</p></td>
    <td align="left"><p>重试</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>Frame 控件</p></td>
    <td align="left"><p>电源管理</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>Frame 控件</p></td>
    <td align="left"><p>更多的数据</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>Frame 控件</p></td>
    <td align="left"><p>受保护的帧</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>Frame 控件</p></td>
    <td align="left"><p>顺序</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>持续时间/ID</p></td>
    <td align="left"></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>地址 1</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>地址 2</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>地址为 3</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>序列控制</p></td>
    <td align="left"><p>片段数</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>序列控制</p></td>
    <td align="left"><p>序列号</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    </tbody>
    </table>

     

-   IHV 扩展 DLL 调用[ **Dot11ExtSendPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff547563)函数来发送通过无线 LAN (WLAN) 适配器的数据包。 DLL 将传递一个唯一的句柄值，该值标识对该函数的数据包*hSendCompletion*参数。 DLL 通常情况下，将包含到数据包的已分配缓冲区的地址传递*hSendCompletion*参数。
    **请注意**  可以通过调用发送仅单播数据包[ **Dot11ExtSendPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff547563)函数。

     

-   当将 WLAN 适配器已发送数据包时，操作系统将调用[ *Dot11ExtIhvSendPacketCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff547516)函数。 操作系统数据包的句柄将值传递给*hSendCompletion*函数的参数。 此句柄值将为 IHV 扩展 DLL 对其调用中使用的相同值[ **Dot11ExtSendPacket**](https://msdn.microsoft.com/library/windows/hardware/ff547563)。

    当[ *Dot11ExtIhvSendPacketCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff547516)是调用，IHV 扩展 DLL 必须释放它分配了数据包的内存。

    **请注意**  IHV 扩展 DLL 必须释放为通过发送的数据包分配的资源[ **Dot11ExtSendPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff547563)直到相应地调用[*Dot11ExtIhvSendPacketCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff547516)进行。

     

 

 





