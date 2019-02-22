---
title: NetworkDirect 断开连接方案
description: 本部分介绍的 NetworkDirect 断开连接方案
ms.assetid: A7973588-5AED-494E-92CA-D5EFB2C7950A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1a96c82c7ce74f3d9d36b4eff463ff11978b018
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540463"
---
# <a name="networkdirect-disconnect-scheme"></a>NetworkDirect 断开连接方案


此处所述的方案适用于[NDSPI](https://msdn.microsoft.com/library/cc904391)版本 2 和[NDKPI](network-direct-kernel-programming-interface--ndkpi-.md)。 使用以下术语：

-   ND 用于引用 NDSPI 或 NDK。
-   *NdDisconnect*用于指 ND 使用者发出才能启动正常断开连接的函数调用。 对于 NDSPI，这是[ **INDConnector::Disconnect**](https://msdn.microsoft.com/library/cc904364)。 对于 NDKPI，它是*NdkDisconnect* ([*NDK\_FN\_断开连接*](https://msdn.microsoft.com/library/windows/hardware/hh439885))。
-   *NdDisconnectIndication*用于引用时 ND 提供程序接收正常 ND 提供程序向 ND 使用者提供的指示从对等方断开连接，或者检测到由于任何原因 （而不是本地已中止连接NDK 使用者拥有如发出的用于启动*NdDisconnect*或*NdCloseConnector*)。

下面，A 和 B 是指 ND 连接的两个方面。 使用者的引用 ND 使用者端 A 上，提供一个程序是指上一侧的 ND 提供程序，并同样使用者 B/提供程序 B 是指在端 B.这些相同的实体当使用者一个调用*NdDisconnect*，提供程序必须发送一个正常断开连接 B 端的通知，然后完成使用者一个*NdDisconnect*请求仅当两个以下条件发生：

-   二者之一：
    -   正常断开连接的通知接收从 B (这会导致的使用者 A 的成功完成*NdDisconnect*)，或
    -   错误，如连接 abortion 或超时发生 (这会导致 A 的使用者*NdDisconnect*以已完成，但失败)。
-   QP 上的所有 DMA 活动已都完成 （包括使用无提示成功标志发布的工作请求的 DMA 活动）。

当提供程序 B 收到正常断开连接的通知或检测到连接已中止，则必须提供提供程序 B *NdDisconnectIndication*到 B，如果使用者 B 具有未调用的使用者*NdDisconnect*提供程序 B 已到。 自传入正常断开连接通知或中止事件可以与启动本地使用者竞争*NdDisconnect*，本地使用者必须准备好处理*NdDisconnectIndication*在本地使用者调用后到达*NdDisconnect*。 请注意， *NdDisconnectIndication*不提供任何保证方面的工作请求完成。

不能重复使用者使用断开连接的 QP 或连接器。

NetworkDirect 不具有任何概念半关闭连接。 一次*NdDisconnect*完成 （与成功或失败），完全关闭连接。

使用者通常应调用*NdDisconnect*仅获取的所有工作请求完成后发送到发起方队列。 否则为*NdDisconnect*可能不会导致，则返回 true 的正常断开连接。 提供程序都不需要支持正常断开连接在其中使用者离开此类工作请求未完成的情况下。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






