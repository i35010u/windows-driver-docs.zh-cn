---
title: WDI 微型端口驱动程序设计指南
description: WLAN 设备驱动程序接口 (WDI) 是用于桌面版本中 （主页、 专业版、 企业版和教育） 这两个 Windows 10 和 Windows 10 移动版的新 WLAN 通用 Windows 驱动程序模型。
ms.assetid: E1666D5E-1932-4378-B4F6-61F28716183E
keywords:
- wi-fi 驱动程序、 wi-fi 驱动程序 Windows 10、 无线驱动程序、 无线驱动程序 windows 10，wlan 驱动程序、 wlan 驱动程序 windows 10，wlan 驱动程序接口、 WDI 驱动程序、 WDI 网络驱动程序，WDI Windows 10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30576a70791634c954a809c0ffcb5a400b843c63
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387205"
---
# <a name="wdi-miniport-driver-design-guide"></a>WDI 微型端口驱动程序设计指南


WLAN 设备驱动程序接口 (WDI) 是 Wi-fi 驱动程序、 桌面版本中 （主页、 专业版、 企业版和教育） 这两个 Windows 10 和 Windows 10 移动版的新通用 Windows 驱动程序模型。 WLAN 设备制造商将写入 WDI 微型端口驱动程序，以使用 Windows 10 操作系统实现。 WDI 能够进行设备制造商可以编写更少的代码比以前的本机 WLAN 驱动程序模型。 Windows 10 中引入的所有新 WLAN 功能均需要基于 WDI 的驱动程序。

供应商提供的本机 WLAN 驱动程序继续在 Windows 10 中运行，但功能仅限于开发它们时所针对的 Windows 版本。

WDI 要求和接口规范记录在此设计指南。 新模型的主要目标是：

-   提高质量和可靠性的 Windows WLAN 驱动程序。
-   减少当前驱动程序模型，这又降低了 IHV 驱动程序的复杂性并减少 IHV 驱动程序开发的总成本的复杂性。

本文档的重点是指定的流和 Windows 和 IHV 驱动程序组件之间的 Wi-fi 操作行为。 它不涵盖软件界面签名 （例如，设备驱动程序接口模型） 和有关如何在 Windows 中加载 IHV 组件的详细信息。

## <a name="design-principles"></a>设计原则


以下原则指导的整体模型和设计此协议。

1.  最小化的主机组件和 IHV 组件/设备之间的通信的通信频率。 这是特别重要的实现如 SDIO 总线上即本质上是琐碎。
2.  应由设备的 Wi-fi 功能 （尤其是必须较低的延迟执行的功能）。
3.  所有法规相关的功能驻留在 IHV 组件，并由 IHV 控制。
4.  由宿主组件和 Windows 操作系统控制的 Windows 体验。
5.  Windows 具有恢复挂起的设备的功能。 它具有足够的状态来对 IHV 组件并在 10 秒内恢复。
6.  由主机处理需要大量的系统内存或速度快的处理器，而不特定于供应商的操作。

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
<td align="left"><p>连接到总线的硬件完整作品。 设备可在其中 （值得注意的是 Wi-fi 和蓝牙） 具有多个无线收发器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Wi-fi 适配器</p></td>
<td align="left"><p>此规范中所述实现的 Wi-fi 功能的设备的特定部分。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Port</p></td>
<td align="left"><p>表示一个特定连接的 MAC 和物理状态的对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IHV 组件</p></td>
<td align="left"><p>表示到主机的 Wi-fi 适配器/设备 IHV 开发的软件组件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>主机</p></td>
<td align="left"><p>主机端 Microsoft/运行系统交互的软件与 IHV 组件使用此规范中描述的接口。</p></td>
</tr>
<tr class="even">
<td align="left"><p>上边缘驱动程序 (UE)</p></td>
<td align="left"><p>UE 指 WdiWiFi 驱动程序，在本文档中称为 WDI。 UE 和较低的边缘 (LE) IHV 驱动程序将合并为完整的 NDIS 微型端口驱动程序。 UE 实现核心 Wi-fi 逻辑。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>较低边缘驱动程序 (LE)</p></td>
<td align="left"><p>LE 指下边缘处的 IHV 驱动程序。 LE 和 UE 将合并为完整的 NDIS 微型端口驱动程序。 LE 实现总线和硬件特定的函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>功能级别重置 (FLR)</p></td>
<td align="left"><p>功能级别重置，如 PCIe 规范中所示。 此术语是指重置的函数，而不是完整的设备，这可能有一个复合函数的重置。 此类作用域的重置不能影响同一设备上的其他函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>平台级别重置 (PLR)</p></td>
<td align="left"><p>平台级别重置。 重置此设置方法影响的设备上的所有函数。 它是非常普遍，以降低成本和占地面积的设备上生成多个函数。 例如，蓝牙通常内置到 wi-fi 芯片上。 但是，这种重置方法重置设备上的所有函数单位。</p></td>
</tr>
<tr class="even">
<td align="left"><p>重置恢复 (RR)</p></td>
<td align="left"><p>RR 是指重置和恢复的事件序列。</p>
<p>对于 FLR，这包括：</p>
<ul>
<li>到 NDIS，将请求转发到总线以重置的 Wi-fi 函数请求。</li>
<li>固件上下文由驱动程序的恢复。</li>
<li>如果它已连接之前重置的访问点的重新连接。</li>
</ul>
<p>对于 PLR，这包括：</p>
<ul>
<li>到 NDIS，将其转发给总线请求。 与即插即用交互总线意外删除设备。</li>
<li>设备重新枚举。</li>
<li>重新建立设备堆栈。</li>
<li>Wi-fi 重启并重新连接。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>WDI 命令</p></td>
<td align="left"><p>UE 发送 WDI Oid 并调用 LE 回调。 所有这些称为 WDI 命令。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MAC 地址随机化</p></td>
<td align="left"><p>为了改进 Windows 10 用户，配置的隐私的 Wi-fi MAC 地址用于在某些情况下，如连接到特定的 Wi-fi 网络或在特定条件启动的扫描之前。 这仅适用于站端口。 系统可确保相应地，使用该随机化因此重要连接方案不是乱码。 系统管理地址发生更改，通过发出<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-dot11-reset" data-raw-source="[OID_WDI_TASK_DOT11_RESET](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-dot11-reset)">OID_WDI_TASK_DOT11_RESET</a>命令之前发出一次扫描，或连接命令。 重置命令参数包括一个可选参数，MAC 地址。 如果存在参数，则 MAC 地址重置为指定的值。 如果它不存在，MAC 地址将保持为当前值。 在配置随机的 MAC 地址时，操作系统使用 IEEE802 地址定义的"本地管理的"格式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ECSA</p></td>
<td align="left"><p>扩展的通道交换机公告。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题


[WDI 微型端口驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

 

 






