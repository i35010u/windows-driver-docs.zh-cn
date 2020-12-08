---
title: 不在用户界面中显示的关键字
description: 不在用户界面中显示的关键字
keywords:
- 安装关键字 WDK 网络，不可见
- 不可见的关键字 WDK DNIS 微型端口
- 隐藏关键字 WDK DNIS 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f64564d809a7b049b563bbf7a65119d41db7de60
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789727"
---
# <a name="keywords-not-displayed-in-the-user-interface"></a>不在用户界面中显示的关键字





Ndis 6.0 和更高版本的 NDIS 为网络设备的微型端口驱动程序提供了一些标准化关键字。 这些标准化关键字显示在 INF 文件中，而不是在用户界面中显示。

下面的列表中介绍了这些常规关键字。 有关特定关键字的详细信息，请在 WDK 文档中搜索关键字。

<a href="" id="-iftype"></a>**\*IfType**  
设备的 NDIS 接口类型。 有关 NDIS 接口类型的详细信息，请参阅 [Ndis 接口类型](./ndis-interface-types.md)。

<a href="" id="-mediatype"></a>**\*MediaType**  
设备的媒体类型。 有关微型端口适配器的媒体类型的详细信息，请参阅 [ \_ \_ \_ 支持 OID 生成媒体](./oid-gen-media-supported.md)。

<a href="" id="-physicalmediatype"></a>**\*PhysicalMediaType**  
设备的物理媒体类型。 有关微型端口适配器的物理媒体类型的详细信息，请参阅 [OID \_ GEN \_ 物理 \_ 介质](./oid-gen-physical-medium.md)。

<a href="" id="-ndisdevicetype-------"></a>**\*NdisDeviceType**   
设备的类型。 默认值为零，表示连接到网络的标准网络设备。 **\*** \_ \_ \_ 如果此设备是终结点设备，并且不是连接到网络的真正网络接口，请将 NdisDeviceType 设置为 NDIS 设备类型终结点 (1) 。 例如，你必须 \_ \_ \_ 为设备（例如智能手机）指定 NDIS 设备类型终结点，以便使用网络基础结构与本地计算机系统通信，但不提供与外部网络的连接。 但是， **\* 不 \*** 能将此关键字设置为虚拟适配器（如 VPN 接口）的 NDIS_DEVICE_TYPE_ENDPOINT，因为它们提供了与外部网络的连接。

**注意**  Windows Vista 自动标识和监视计算机连接到的网络。 如果设置了 NDIS \_ 设备 \_ 类型 \_ 终结点标志，则设备是终结点设备，并且不与真正的外部网络建立连接。 因此，Windows 在识别网络时将忽略终结点设备。 网络感知 Api 表明设备不将计算机连接到网络。 对于这种情况下的最终用户而言，通知区域中的 "网络和共享中心" 和 "网络" 图标不会将 NDIS 终结点设备显示为已连接。 不过，连接显示在 "网络连接" 文件夹中。


 

