---
title: 供应商提供的 DCB 组件
description: 供应商提供的 DCB 组件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a419dcb50c49d175b930b9a504b0e51fbd06b8ad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808013"
---
# <a name="vendor-provided-dcb-components"></a>供应商提供的 DCB 组件


本部分介绍 (DCB) 的用于 IEEE 802.1 数据中心桥接的 NDIS 服务 (QoS) 体系结构中的各种组件。 下图显示了这些组件。

![设备安装组件](images/dcb.png)

该图中的阴影框表示独立硬件供应商 (Ihv) 和原始设备制造商 (Oem) 提供的 DCB 组件。 以下列表描述了这些组件：

<a href="" id="link-layer-discovery-protocol--lldp--agent"></a> (LLDP) 代理的链接层发现协议  
从 Windows Server 2012 开始，支持 IEEE 802.1 Qaz DCB Exchange (DCBX) 协议的供应商可为对其执行802.1 的 IEEE qab DCBX LLDP 协议提供支持。 可以通过微型端口驱动程序或 LLDP 代理提供此 LLDP 支持。

通常，LLDP agent 和 DCB 微型端口驱动程序通过专用控制路径进行通信，如专用 i/o 控制 (IOCTL) 接口。

如果供应商提供 LLDP 代理，我们强烈建议在用户模式下运行代理，以减轻与处理网络数据包相关的一般稳定性风险。

<a href="" id="fibre-channel-over-ethernet--fcoe--initiator"></a>通过以太网 (FCoE) 发起程序的光纤通道  
Windows 操作系统本身并不支持 FCoE。 为支持 FCoE，供应商必须提供用于连接到远程存储设备的 FCoE 发起程序堆栈。

<a href="" id="dcb-capable-miniport-driver-and-network-adapter"></a>支持 DCB 的微型端口驱动程序和网络适配器  
为支持 DCB 的 NDIS QoS，微型端口驱动程序和网络适配器必须支持 [Ndis Qos 要求中描述的数据中心桥接](ndis-qos-requirements-for-data-center-bridging.md)的要求。

 

 





