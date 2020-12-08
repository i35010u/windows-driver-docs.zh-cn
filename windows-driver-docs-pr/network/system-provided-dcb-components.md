---
title: 系统提供的 DCB 组件
description: 系统提供的 DCB 组件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d91026b56259c646fa74a0acde4ee0c55b494d79
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837909"
---
# <a name="system-provided-dcb-components"></a>系统提供的 DCB 组件


本部分介绍 (DCB) 的用于 IEEE 802.1 数据中心桥接的 NDIS 服务 (QoS) 体系结构中的各种组件。 下图显示了这些组件。

![设备安装组件](images/dcb.png)

关系图中的 unshaded 框表示 Windows 操作系统提供的模块。 具体而言，操作系统提供支持 DCB 的以下模块：

<a href="" id="network-qos-policy-wmi-provider"></a>网络 QoS 策略 WMI 提供程序  
此模块提供了一个接口，用于 Windows Management Instrumentation (WMI) 客户端在操作系统的网络堆栈中查询和设置基于 QoS 的网络策略。 这些策略允许将特定类型的网络流量分配给 DCB 流量类，以便进行传输、 *传出*、管理和优先级传递。

网络策略定义一组条件和操作。 与条件匹配的出口数据包（例如 TCP 或 UDP 端口号）会分配与条件相关的操作。 从 NDIS 6.30 开始，策略操作指定已为其分配 DCB 流量类的 802.1 p 优先级别。

网络 QoS 策略是 NDIS QoS 分类的超集。 只要策略条件和操作与 NDIS QoS 分类元素的限制匹配，使用网络策略 WMI 提供程序定义的策略可能会自动迁移到 NDIS QoS。 有关这些元素的详细信息，请参阅 [NDIS QoS 流量分类](ndis-qos-traffic-classifications.md)。

此 WMI 提供程序将网络策略保存在系统注册表的单独存储区中。

<a href="" id="dcb-wmi-provider"></a>DCB WMI 提供程序  
此组件为 WMI 客户端提供了一个接口，用于查询和设置基础微型端口驱动程序上的 NDIS QoS 参数。 通过基于 WMI 的 PowerShell cmdlet 和 WMI 方法，客户端可以在支持 DCB 的微型端口驱动程序上配置 DCB 功能，如基于优先级的流控制 (PFC) 和增强的传输选择 (ETS) 。

<a href="" id="dcb"></a>DCB  
 ( # A0) 的 DCB 组件配置支持 DCB 的微型端口驱动程序与 DCB 参数设置。 DCB 组件从以下来源获取这些设置：

-   系统注册表中 DCB 策略存储的持久设置。

-   来自 DCB WMI 用户模式提供程序的动态设置。 这些设置在 DCB WMI 提供程序和 DCB 模块之间 (IOCTL) 接口的专用 i/o 控件上传递。

DCB 组件还将 QOS 分类设置从 QIM 组件中继到支持 NDIS QoS 的微型端口驱动程序。

<a href="" id="qos-inspection-module--qim-"></a>QoS 检查模块 (QIM)   
QIM 组件是核心 TCP/IP 网络堆栈中的数据包检查层的一部分 ( # A0) 。 从 Windows Server 2012 开始，此组件会为流量优先级执行基于 QoS 的数据包分类。

QIM 组件)  (公开专用网络编程接口。 当 DCB 组件在基础微型端口驱动程序上设置 QoS 参数时，它会通过此 NPI 接口将这些设置中继到 QIM 组件。 这允许 DCB 在 QIM 中创建基于 DCB 应用程序优先级设置的 QoS 策略。 有关 NPI 接口的详细信息，请参阅 [网络编程接口](network-programming-interface.md)。

QIM 组件还处理注册表中策略存储中的网络 QoS 策略。 如果这些策略与 NDIS QoS 分类元素兼容，则 QIM 组件将在 NPI 接口上迁移策略，并将其发布到 DCB 组件。

**注意**  QIM 组件创建的策略将进入活动存储区，并且不会在系统重新启动后保持。

 

**注意**  从 Windows Server 2012 开始，默认情况下不会安装 DCB 和 DCB WMI 提供程序组件。 这些组件通过安装 Microsoft DCB server 功能进行安装和启用。 此功能通过使用服务器管理器的 "添加角色和功能向导" 来安装。

 

 

 





