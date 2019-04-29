---
title: NDIS 端口的类型
description: NDIS 端口的类型
ms.assetid: a77ceb1b-d4b9-4a42-aa5b-685295722fa3
keywords:
- 端口 WDK NDIS，类型
- NDIS 端口 WDK，类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50afb12241b115c8a95bdc4778e8d6a06dd5d977
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358273"
---
# <a name="types-of-ndis-ports"></a>NDIS 端口的类型





NDIS 端口可以是以下类型之一：

<a href="" id="ndisporttypeundefined"></a>**NdisPortTypeUndefined**  
默认端口类型。 使用此类型的常规端口应用程序不适合以下类型之一。

<a href="" id="ndisporttypebridge"></a>**NdisPortTypeBridge**  
保留供系统使用。

<a href="" id="ndisporttyperasconnection"></a>**NdisPortTypeRasConnection**  
远程访问服务 (RAS) 连接。

<a href="" id="ndisporttype8021xsupplicant"></a>**NdisPortType8021xSupplicant**  
远程的无线工作站与此主机计算机上的访问点相关联。

<a href="" id="ndisporttypendisimplatform"></a>**NdisPortTypeNdisImPlatform**  
保留供系统使用。

**请注意**  仅在 NDIS 6.30 和更高版本支持此值。

 

NDIS 端口的特征不同于到另一个端口应用程序。 例如，对于桥接接口，微型端口驱动程序的上边缘中间的驱动程序创建**NdisPortTypeBridge**时协议缘中间驱动程序绑定到物理微型端口适配器所需的端口桥接在三层。

## <a name="related-topics"></a>相关主题


[NDIS 端口](ndis-ports.md)

[NDIS 端口的概述](overview-of-ndis-ports.md)

 

 






