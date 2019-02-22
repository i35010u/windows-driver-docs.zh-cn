---
title: 供应商提供 DCB 组件
description: 供应商提供 DCB 组件
ms.assetid: 864BB701-352A-4F61-934C-3E4E8EEE02C5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7c0d9a528753533e56946315f5f962c10a644c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521872"
---
# <a name="vendor-provided-dcb-components"></a>供应商提供 DCB 组件


本部分介绍 NDIS 服务质量 (QoS) 体系结构的 IEEE 802.1 数据中心桥接 (DCB) 的一部分的各种组件。 这些组件在下图中显示。

![设备安装组件](images/dcb.png)

阴影框中的关系图表示 DCB 组件的独立硬件供应商 (Ihv) 和原始设备制造商 (Oem) 提供。 以下列表介绍了这些组件：

<a href="" id="link-layer-discovery-protocol--lldp--agent"></a>链接层发现协议 (LLDP) 代理  
从 Windows Server 2012，供应商支持 IEEE 802.1Qaz 开始 DCB 交换 (DCBX) 协议可以对其执行 DCBX IEEE 802.1Qab LLDP 协议提供支持。 可以通过微型端口驱动程序或 LLDP 代理提供此 LLDP 支持。

通常情况下，LLDP 代理和支持 DCB 的微型端口驱动程序进行通信通过专用控件的路径，例如专用的 I/O 控制 (IOCTL) 的接口。

如果供应商提供 LLDP 代理，我们强烈建议将代理驻留在用户模式下，若要缓解与网络数据包处理相关的常规稳定性风险。

<a href="" id="fibre-channel-over-ethernet--fcoe--initiator"></a>通过以太网 (FCoE) 发起程序的光纤通道  
Windows 操作系统不以本机方式支持 FCoE。 若要支持 FCoE，供应商必须提供用于连接到远程存储设备的 FCoE 发起程序堆栈。

<a href="" id="dcb-capable-miniport-driver-and-network-adapter"></a>支持 DCB 的微型端口驱动程序和网络适配器  
若要支持 DCB 的 NDIS QoS，微型端口驱动程序和网络适配器必须支持中所述的要求[的数据中心桥接的 NDIS QoS 要求](ndis-qos-requirements-for-data-center-bridging.md)。

 

 





