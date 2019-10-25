---
title: WDI 微型端口驱动程序设计指南
description: 对于桌面版的 Windows 10 （家庭版、专业版、企业版和教育版）和 Windows 10 移动版，WLAN 设备驱动程序接口（WDI）是新的 WLAN 通用 Windows 驱动程序模型。
ms.assetid: E1666D5E-1932-4378-B4F6-61F28716183E
keywords:
- wi-fi 驱动程序，wi-fi 驱动程序 Windows 10，无线驱动程序，无线驱动程序 windows 10，wlan 驱动程序，wlan 驱动程序 windows 10，wlan 驱动程序接口，WDI 驱动程序，WDI 网络驱动程序，WDI Windows 10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 789cfeb9ab90e94f817bd7f846e6277573ecb135
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842919"
---
# <a name="wdi-miniport-driver-design-guide"></a>WDI 微型端口驱动程序设计指南


WLAN 设备驱动程序接口（WDI）是适用于 Wlan 驱动程序的新的通用 Windows 驱动程序模型，适用于适用于桌面版的 Windows 10 （家庭版、专业版、企业版和教育版）以及 Windows 10 移动版。 WLAN 设备制造商编写了 WDI 微型端口驱动程序，以便使用 Windows 10 OS 实现。 WDI 使设备制造商可以编写比以前的本机 WLAN 驱动程序模型更少的代码。 Windows 10 中引入的所有新 WLAN 功能均需要基于 WDI 的驱动程序。

供应商提供的本机 WLAN 驱动程序继续在 Windows 10 中运行，但功能仅限于开发它们时所针对的 Windows 版本。

此设计指南中记录了 WDI 要求和接口规范。 新模型的主要目标是：

-   提高 Windows WLAN 驱动程序的质量和可靠性。
-   降低当前驱动程序模型的复杂性，进而降低 IHV 驱动程序的复杂性并降低 IHV 驱动程序开发的总体成本。

本文档的重点是在 Windows 和 IHV 驱动程序组件之间指定 Wi-fi 操作的流和行为。 它不涵盖软件接口签名（例如，设备驱动程序接口模型）以及有关如何在 Windows 中加载 IHV 组件的详细信息。

## <a name="design-principles"></a>设计原则


以下原则指导了此协议的整体模型和设计。

1.  最大程度地减少主机组件与 IHV 组件/设备之间的流量交互成本。 这对于在本质上很繁琐的总线（如 SDIO）上的实现尤其重要。
2.  Wi-fi 功能（尤其是必须以低延迟时间执行的功能）应由设备处理。
3.  所有规章相关功能都驻留在 IHV 组件中，由 IHV 控制。
4.  Windows 体验由主机组件和 Windows 操作系统控制。
5.  Windows 能够恢复挂起的设备。 它的状态足以使 IHV 组件重新编程，并在10秒内恢复。
6.  需要大量系统内存或快速处理器而不是特定于供应商的操作由主机处理。

## <a name="definitions"></a>定义


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>设备</p></td>
<td align="left"><p>连接到总线的整个硬件。 一台设备可以有多个收音机（特别是 Wi-fi 和蓝牙）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Wi-fi 适配器</p></td>
<td align="left"><p>实现 Wi-fi 功能的设备的特定部分，如本规范中所述。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>端口</p></td>
<td align="left"><p>一个对象，该对象表示特定连接的 MAC 和 PHY 状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IHV 组件</p></td>
<td align="left"><p>IHV 开发的软件组件，它将 Wi-fi 适配器/设备表示到主机。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Host</p></td>
<td align="left"><p>使用此规范中所述的接口与 IHV 组件进行交互的主机端/操作系统软件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>上边缘驱动程序（UE）</p></td>
<td align="left"><p>UE 指的是 WdiWiFi 驱动程序（在本文档中名为 WDI）。 UE 和下边缘（LE） IHV 驱动程序组合成一个完整的 NDIS 微型端口驱动程序。 UE 实现核心 Wi-fi 逻辑。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>下边缘驱动程序（LE）</p></td>
<td align="left"><p>LE 指的是位于下边缘的 IHV 驱动程序。 LE 和 UE 组合到一个完整的 NDIS 微型端口驱动程序中。 该 LE 实现了总线和硬件特定的功能。</p></td>
</tr>
<tr class="even">
<td align="left"><p>功能级别重置（FLR）</p></td>
<td align="left"><p>功能级别重置，如 PCIe 规范中所示。 此术语是指重置函数，而不是对可能具有复合函数的完整设备进行重置。 此类作用域的重置不会影响同一设备上的其他功能。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>平台级别重置（PLR）</p></td>
<td align="left"><p>平台级别重置。 此 reset 方法会影响设备上的所有功能。 在设备上构建多种功能非常受欢迎，可降低成本和占用空间。 例如，蓝牙通常是使用 Wi-fi 在芯片上构建的。 但是，这种重置方法将重置设备上的所有功能单元。</p></td>
</tr>
<tr class="even">
<td align="left"><p>重置恢复（RR）</p></td>
<td align="left"><p>RR 指重置和恢复事件的顺序。</p>
<p>对于 FLR，这包括：</p>
<ul>
<li>向 NDIS 发出的请求，该请求将请求转发到总线以重置 Wi-fi 函数。</li>
<li>驱动程序恢复固件上下文。</li>
<li>如果在重置之前已连接到访问点，则重新连接到该访问点。</li>
</ul>
<p>对于 PLR，这包括：</p>
<ul>
<li>向 NDIS 发出请求的请求，该请求将请求转发到总线。 总线与 PnP 交互以意外删除设备。</li>
<li>重新枚举设备。</li>
<li>重新建立设备堆栈。</li>
<li>Wi-fi 重新启动并重新连接。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>WDI 命令</p></td>
<td align="left"><p>UE 发送 WDI Oid，并调用 LE 回调。 所有这些命令均称为 WDI 命令。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MAC 地址随机化</p></td>
<td align="left"><p>为了提高 Windows 10 用户的隐私性，在某些情况下（例如，在连接到特定的 Wi-fi 网络之前，或在特定条件下启动扫描时），会使用配置的 Wi-fi MAC 地址。 这仅适用于工作站端口。 系统确保正确使用随机化，因此重要的连接方案不会中断。 系统通过在发出 scan 或 connect 命令之前发出<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-dot11-reset" data-raw-source="[OID_WDI_TASK_DOT11_RESET](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-dot11-reset)">OID_WDI_TASK_DOT11_RESET</a>命令来管理地址的更改。 Reset 命令参数包含可选的 MAC 地址参数。 如果参数存在，则将 MAC 地址重置为指定的值。 如果它不存在，则将 MAC 地址留给当前值。 配置随机 MAC 地址时，操作系统使用为 IEEE802 地址定义的 "本地管理" 格式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ECSA</p></td>
<td align="left"><p>扩展通道交换机公告。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题


[WDI 微型端口驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

 

 






