---
title: 要求和限制适用于 IPsec 卸载
description: 要求和限制适用于 IPsec 卸载
ms.assetid: c016d6dd-f760-4340-8d56-9bd69e4fe84e
keywords:
- ESP 保护数据包 WDK IPsec 卸载、 要求
- AH 保护数据包 WDK IPsec 卸载、 要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d739bf72342434c1b6e8e2cd97273f191d5b97e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555711"
---
# <a name="requirements-and-restrictions-that-apply-to-ipsec-offloads"></a>要求和限制适用于 IPsec 卸载

\[IPsec 任务卸载功能已弃用，不应使用。\]




以下要求和限制适用于 Internet 协议安全性 (IPsec) 卸载：

-   NIC 必须维护安全关联 (SA) 表。 这可以提高性能，无需包含密钥或 AH 和 ESP 中处理所需的其他信息将数据包发送。

-   一个 NIC 可能能够处理单个数据包 AH 和 ESP 有效负载。 在这种情况下，NIC 必须支持的 AH 和 ESP 完整性 （身份验证） 算法的以下可能的组合：

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
    <td align="left"><p>Null （仅当 NIC 支持 null 加密）</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>SHA 1</p></td>
    <td align="left"><p>Null （仅当 NIC 支持 null 加密）</p></td>
    </tr>
    </tbody>
    </table>

     

<!-- -->

-   支持 DES 算法的 NIC 必须生成需要这些算法的初始化向量 (IV)。

-   只有 IPsec 执行的任务的 NIC 是处理加密的 AH 校验和或 ESP 校验和 （或两者） 以及加密和解密 ESP 有效负载。 对于发送的数据包，TCP/IP 传输创建所有标头，填充，并重播数字并可选择是唯一的目标地址/IPsec 协议对 SPI 值。 为接收数据包、 TCP/IP 传输执行入站的策略检查、 句柄重播检测和防护、 和句柄审核事件。

-   对于发送数据包时，TCP/IP 传输不提供确切的偏移量 （例如，指示加密数据的起始） 因为卸载驱动程序可以轻松地确定此信息从它使用到的特定安全关联 (SA) 进程数据包。

-   使用 IPsec 协议数据包必须具有的身份验证标头 (AH) 或封装安全有效负载 (ESP) 标头 （或两者） 中的身份验证信息。 不允许用于 IPsec 数据包能够不进行身份验证。

-   需要 IP 碎片发送数据包或将不会卸载 IPsec 任务接收需要从 IP 碎片重组的数据包。

-   IPsec 任务将不会卸载为发送和接收经过负载平衡的微型端口驱动程序的数据包。 有关负载平衡的详细信息，请参阅[负载平衡和故障转移](https://msdn.microsoft.com/library/windows/hardware/ff549197)。

 

 





