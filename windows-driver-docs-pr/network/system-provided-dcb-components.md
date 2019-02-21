---
title: 系统提供 DCB 组件
description: 系统提供 DCB 组件
ms.assetid: 64C9ADEF-5512-41E4-AE7B-DFEF1B94FC5F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e93641c8fab50e335a98ec96c69261e5fd3589b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546495"
---
# <a name="system-provided-dcb-components"></a>系统提供 DCB 组件


本部分介绍 NDIS 服务质量 (QoS) 体系结构的 IEEE 802.1 数据中心桥接 (DCB) 的一部分的各种组件。 这些组件在下图中显示。

![设备安装组件](images/dcb.png)

在关系图中的无阴影的框表示 Windows 操作系统提供的模块。 具体而言，操作系统提供了支持 DCB 的以下模块：

<a href="" id="network-qos-policy-wmi-provider"></a>网络 QoS 策略 WMI 提供程序  
此模块提供了一个接口，使 Windows Management Instrumentation (WMI) 客户端以查询和设置基于 QoS 的网络策略在操作系统的网络堆栈中。 这些策略允许特定类型的网络流量，以便分配给用于传输，DCB 流量类或*出口*，管理和优先的传送。

网络策略定义一组条件和操作。 匹配条件，例如 TCP 或 UDP 端口号的传出数据包分配给条件相关的操作。 策略操作是从 NDIS 6.30 开始，指定已向其分配 DCB 流量类的 802.1p 优先级级别。

网络 QoS 策略是 NDIS QoS 分类的一个超集。 使用网络策略 WMI 提供程序中定义的策略可能会自动迁移到 NDIS QoS，只要策略条件和操作匹配的 NDIS QoS 分类元素的限制。 有关这些元素的详细信息，请参阅[NDIS QoS 流量分类](ndis-qos-traffic-classifications.md)。

此 WMI 提供程序将在系统注册表中保存在独立的存储库中的网络策略。

<a href="" id="dcb-wmi-provider"></a>DCB WMI 提供程序  
此组件提供的 WMI 客户端以查询和设置基础微型端口驱动程序的 NDIS QoS 参数的接口。 通过基于 WMI 的 PowerShell cmdlet 和 WMI 方法，客户端可以支持 DCB 的微型端口驱动程序上配置 DCB 功能，如基于优先级的流控制 (PFC) 和增强传输选择 (ETS)。

<a href="" id="dcb"></a>DCB  
DCB 组件 (Msdcb.sys) 使用 DCB 参数设置来配置支持 DCB 的微型端口驱动程序。 DCB 组件从以下来源获取这些设置：

-   DCB 策略从永久设置存储在系统注册表中。

-   从 DCB WMI 用户模式提供程序的动态设置。 通过专用的 I/O 控制 (IOCTL) 接口 DCB WMI 提供程序和 DCB 模块之间传递这些设置。

DCB 组件还中继 QIM 组件从微型端口驱动程序的支持 NDIS QoS QOS 分类设置。

<a href="" id="qos-inspection-module--qim-"></a>QoS 检查模块 (QIM)  
QIM 组件是核心 TCP/IP 网络堆栈 (Tcpip.sys) 的数据包检查层的一部分。 从 Windows Server 2012 开始，此组件执行通信优先级的基于 QoS 数据包分类。

QIM 组件公开专用网络编程接口 (NPI)。 DCB 组件基础微型端口驱动程序上设置 QoS 参数，它通过此 NPI 接口中继到 QIM 组件的这些设置。 这样，DCB 基于 DCB 应用程序优先级设置的 QIM 中创建 QoS 策略。 有关 NPI 接口的详细信息，请参阅[网络编程接口](network-programming-interface.md)。

QIM 组件还处理从注册表中的策略存储区的网络 QoS 策略。 如果这些策略与 NDIS QoS 分类元素兼容，QIM 组件迁移策略，并通过 NPI 接口向 DCB 组件进行颁发。

**请注意**  QIM 组件创建的策略转到活动的存储，并通过重新启动系统，不会保留。

 

**请注意**  从 Windows Server 2012 开始，未默认情况下安装 DCB 和 DCB WMI 提供程序组件。 安装和启用通过 Microsoft DCB 服务器功能的安装这些组件。 此功能使用的服务器管理器中的添加角色和功能向导进行安装。

 

 

 





