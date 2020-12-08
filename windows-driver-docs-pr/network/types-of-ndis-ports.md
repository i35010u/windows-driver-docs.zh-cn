---
title: NDIS 端口的类型
description: NDIS 端口的类型
keywords:
- 端口 WDK NDIS，类型
- NDIS 端口 WDK，类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c53aca20dd8693fcea98a862ae482266118ce25
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822805"
---
# <a name="types-of-ndis-ports"></a>NDIS 端口的类型





NDIS 端口可以是以下类型之一：

<a href="" id="ndisporttypeundefined"></a>**NdisPortTypeUndefined**  
默认端口类型。 将此类型用于不符合以下任一类型的常规端口应用程序。

<a href="" id="ndisporttypebridge"></a>**NdisPortTypeBridge**  
预留给系统使用。

<a href="" id="ndisporttyperasconnection"></a>**NdisPortTypeRasConnection**  
远程访问服务 (RAS) 连接。

<a href="" id="ndisporttype8021xsupplicant"></a>**NdisPortType8021xSupplicant**  
与此主机计算机上的访问点相关联的远程无线工作站。

<a href="" id="ndisporttypendisimplatform"></a>**NdisPortTypeNdisImPlatform**  
预留给系统使用。

**注意**  此值仅在 NDIS 6.30 和更高版本中受支持。

 

NDIS 端口的特征因端口应用程序而异。 例如，对于桥接口，当中间驱动程序的协议边缘绑定到需要第三层桥的物理微型端口适配器时，中间驱动程序的小型端口驱动程序的上边缘会创建 **NdisPortTypeBridge** 端口。

## <a name="related-topics"></a>相关主题


[NDIS 端口概述](overview-of-ndis-ports.md)

 

 






