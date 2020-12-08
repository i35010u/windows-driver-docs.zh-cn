---
title: 适用于 IPsec 卸载的要求和限制
description: 适用于 IPsec 卸载的要求和限制
keywords:
- 受 ESP 保护的数据包 WDK IPsec 卸载，要求
- 受 AH 保护的数据包 WDK IPsec 卸载，要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f3ecd32d0b75d14ac5257f384c4ef70dca26e5d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837915"
---
# <a name="requirements-and-restrictions-that-apply-to-ipsec-offloads"></a>适用于 IPsec 卸载的要求和限制

\[IPsec 任务卸载功能已弃用，不应使用。\]




以下要求和限制适用于 (IPsec) 卸载的 Internet 协议安全：

-   NIC 必须维护 (SA) 表的安全关联。 这样可以避免在发送数据包中包含 AH 和 ESP 处理所需的密钥或其他信息，从而提高性能。

-   NIC 或许能够处理单个数据包的 AH 和 ESP 负载。 在这种情况下，NIC 必须支持以下可能的完整性组合 (用于 AH 和 ESP 的身份验证) 算法：

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">AH</th>
    <th align="left">ESP</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>MD5</p></td>
    <td align="left"><p>MD5</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>SHA 1</p></td>
    <td align="left"><p>SHA 1</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>MD5</p></td>
    <td align="left"><p>SHA 1</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>SHA 1</p></td>
    <td align="left"><p>MD5</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>MD5</p></td>
    <td align="left"><p>如果 NIC 支持 null 加密，则为 null () </p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>SHA 1</p></td>
    <td align="left"><p>如果 NIC 支持 null 加密，则为 null () </p></td>
    </tr>
    </tbody>
    </table>

     

<!-- -->

-   支持 DES 算法的 NIC 必须生成这些算法所需的初始化向量 (IV) 。

-   NIC 执行的唯一 IPsec 任务是处理加密的 AH 校验和， (或同时) 和加密和解密 ESP 有效负载。 对于发送数据包，TCP/IP 传输会创建所有标头、填充和重播号码，并选择与目标地址/IPsec 协议对唯一的 SPI 值。 对于接收数据包，TCP/IP 传输执行入站策略检查，处理重播检测和预防，并处理审核事件。

-   对于发送数据包，TCP/IP 传输不提供显式偏移 (例如，指示加密数据的开始) ，因为卸载驱动程序可以轻松地从用于处理数据包的特定安全关联 (SA) 来确定此信息。

-   具有 IPsec 协议的数据包必须在身份验证标头中包含身份验证信息 (AH) 或封装安全有效负载 (ESP) 标头 (或两者) 。 不允许 IPsec 数据包进行身份验证。

-   IPsec 任务不会卸载，因此无法发送需要 IP 碎片或需要从 IP 碎片重组的接收数据包的发送数据包。

-   IPsec 任务不会脱离通过负载平衡微型端口驱动程序的发送和接收数据包。 有关负载平衡的详细信息，请参阅 [负载平衡和故障转移](/previous-versions/windows/hardware/network/ff549197(v=vs.85))。

 

