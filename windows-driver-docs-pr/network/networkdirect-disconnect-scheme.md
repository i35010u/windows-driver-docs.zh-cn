---
title: NetworkDirect 断开连接方案
description: 本部分介绍了 NetworkDirect 断开连接方案
ms.assetid: A7973588-5AED-494E-92CA-D5EFB2C7950A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bc4781107992cfc2220dbb76168545fe736d5d2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217016"
---
# <a name="networkdirect-disconnect-scheme"></a>NetworkDirect 断开连接方案


此处所述的方案适用于 [NDSPI](/previous-versions/windows/desktop/cc904391(v=vs.85)) 版本2和 [NDKPI](./overview-of-network-direct-kernel-provider-interface--ndkpi-.md)。 使用了以下术语：

-   ND 用于引用 NDSPI 或 NDK。
-   *NdDisconnect* 用于引用 ND 使用方为启动正常断开连接而进行的函数调用。 对于 NDSPI，这是 [**INDConnector：:D isconnect**](/previous-versions/windows/desktop/cc904364(v=vs.85))。 对于 NDKPI，它是 *NdkDisconnect* ([*NDK \_ FN \_ DISCONNECT*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_disconnect)) 。
-   当 ND 提供程序接收到来自对等方的正常断开连接，或检测到由于任何 (原因而导致连接中止（如颁发*NdDisconnect*或*NdCloseConnector*) ）时， *NdDisconnectIndication*用于引用由 nd 提供程序传递给 nd 使用者的指示。

下面，A 和 B 引用了 ND 连接的双方。 使用者 A 是指侧 A 上的 ND 使用者，提供程序 A 引用侧端的 ND 提供程序，类似于使用者 B/提供程序 B 引用侧 B 上的相同实体。当使用者 A 调用 *NdDisconnect*时，只有当以下两个条件同时出现时，提供商 a 才能将宽容断开连接通知发送到 B 并完成使用者 a 的 *NdDisconnect* 请求：

-   可以是：
    -   从 B (收到宽容断开通知，这会导致成功完成使用者 A 的 *NdDisconnect*) ，或
    -   出现错误，如连接 abortion 或超时 (这会导致使用者 A 的 *NdDisconnect* 完成，并) 失败。
-   QP 上的所有 DMA 活动都已完成 (包括使用缄默成功标志发布的工作请求的 DMA 活动) 。

当提供程序 B 从发出宽容断开连接通知或检测到连接中止时，如果使用者 b 尚未将*NdDisconnect*调用到提供程序 b，则提供程序 b 必须将*NdDisconnectIndication*提供给使用者 b。 由于传入的 "正常断开连接" 通知或中止事件可与本地使用者启动*NdDisconnect*进行争用，因此，本地使用者必须准备好处理在本地使用者调用*NdDisconnect*后到达的*NdDisconnectIndication* 。 请注意， *NdDisconnectIndication* 不会在完成工作请求方面提供任何保证。

使用者无法重新使用断开连接的 QP 或连接器。

NetworkDirect 没有半闭连接的任何概念。 *NdDisconnect*完成后 () 成功或失败，连接将完全关闭。

通常情况下，使用者通常会在其发布到发起方队列的所有工作请求完成后调用 *NdDisconnect* 。 否则， *NdDisconnect* 可能不会导致真正的正常断开连接。 当使用者将此类工作请求挂起时，提供程序不需要支持正常断开连接。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](./overview-of-network-direct-kernel-provider-interface--ndkpi-.md)

 

