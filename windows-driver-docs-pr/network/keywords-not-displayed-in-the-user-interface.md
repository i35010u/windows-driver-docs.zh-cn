---
title: 不在用户界面中显示的关键字
description: 不在用户界面中显示的关键字
ms.assetid: 0d2aeaa3-4e47-413b-907f-5e70b34f0725
keywords:
- 安装关键字 WDK 网络、 不可见
- 非可见关键字 WDK DNIS 微型端口
- 隐藏的关键字 WDK DNIS 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 821d469359adb012f4c2b8227703d7347022206d
ms.sourcegitcommit: a58b4859254a651502e4329a6e521fe0fa11c7f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56582903"
---
# <a name="keywords-not-displayed-in-the-user-interface"></a>不在用户界面中显示的关键字





NDIS 6.0 和更高版本的 NDIS 网络设备的微型端口驱动程序提供一些标准化的关键字。 这些标准化的关键字出现在 INF 文件但不是在用户界面。

以下列表中描述了这些常见的关键字。 有关特定关键字的详细信息，搜索 WDK 文档中的关键字。

<a href="" id="-iftype"></a>**\*IfType**  
设备的 NDIS 接口类型。 有关 NDIS 接口类型的详细信息，请参阅[NDIS 接口类型](https://msdn.microsoft.com/library/windows/hardware/ff565767)。

<a href="" id="-mediatype"></a>**\*MediaType**  
设备的媒体类型。 有关微型端口适配器的媒体类型的详细信息，请参阅[OID\_代\_媒体\_支持](https://msdn.microsoft.com/library/windows/hardware/ff569609)。

<a href="" id="-physicalmediatype"></a>**\*PhysicalMediaType**  
物理媒体类型的设备。 有关微型端口适配器的物理媒体类型的详细信息，请参阅[OID\_代\_物理\_中等](https://msdn.microsoft.com/library/windows/hardware/ff569621)。

<a href="" id="-ndisdevicetype-------"></a>**\*NdisDeviceType**   
设备的类型。 默认值为零，表示连接到网络的标准网络设备。 设置 **\*NdisDeviceType**到 NDIS\_设备\_类型\_终结点 (1) 如果此设备是终结点设备，而不是连接到网络的真实网络接口。 例如，您必须指定 NDIS\_设备\_类型\_使用的网络基础结构与本地计算机系统进行通信，但不是提供到外部连接的智能手机等设备的终结点网络。 但是，必须**\*不\*** 将此关键字设置为 NDIS_DEVICE_TYPE_ENDPOINT 为虚拟适配器，如 VPN 接口，因为它们提供到外部网络的连接。

**请注意**  Windows Vista 会自动识别并监视一台计算机连接到的网络。 如果 NDIS\_设备\_类型\_设置终结点标志，该设备的终结点设备且不是与真实的外部网络的连接。 因此，Windows 将在它识别到网络时忽略终结点设备。 Network Awareness Api 指示该设备不会连接到网络计算机。 对于最终用户在此情况下，网络和共享中心以及通知区域中的网络图标不会显示为已连接的 NDIS 终结点设备。 但是，在网络连接文件夹中显示了连接。


 

 





