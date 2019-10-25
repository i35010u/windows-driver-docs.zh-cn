---
title: Winsock 内核对象
description: Winsock 内核对象
ms.assetid: 1ce9bd19-9159-4a73-96f6-6e2adac886b9
keywords:
- Winsock 内核 WDK 网络，对象
- WSK WDK 网络，对象
- 对象 WDK Winsock 内核
- 套接字对象 WDK Winsock 内核
- 客户端对象 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f84162c203c904ca83121fe57ba3a66497090d6a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844373"
---
# <a name="winsock-kernel-objects"></a>Winsock 内核对象


Winsock 内核（WSK）[网络编程接口（NPI）](network-programming-interface.md)围绕两种主要对象类型进行设计：*客户端*和*套接字*。

<a href="" id="client-object-------"></a>**客户端对象**   
*客户端对象*表示 WSK 应用程序与 WSK 子系统之间的附件。 客户端对象由[**WSK\_的客户端**](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-client)结构表示。 在连接到 WSK 子系统的过程中，指向客户端对象的指针将返回到 WSK 应用程序。 WSK 应用程序将此指针传递到在客户端对象级别操作的所有 WSK 函数。

<a href="" id="socket-object-------"></a>**套接 Object**   
*套接字对象*表示可用于网络 i/o 的网络套接字。 套接字对象由[**WSK\_套接字**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_socket)结构表示。 当应用程序创建新的套接字或应用程序接受传入连接时，指向套接字对象的指针将返回到 WSK 应用程序。 WSK 应用程序将此指针传递给特定于特定套接字的所有 WSK 函数。

 

 





