---
title: 关联后的操作
description: 关联后的操作
ms.assetid: e4c7ea7a-53ad-41b2-bf3f-03c770e58043
keywords:
- IHV 扩展 DLL WDK 本机 802.11，后期关联操作
- 后关联操作 WDK 本机 802.11 IHV 扩展 DLL
- 本机 802.11 IHV 扩展 DLL WDK，后期关联操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cee769a195b5e6168ea2c41bd198f71703709290
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342943"
---
# <a name="post-association-operations"></a>关联后的操作




 

无线 LAN (WLAN) 适配器已成功完成时的访问点 (AP) 的关联操作，操作系统会创建关联的数据端口。 操作系统然后通过调用来启动数据端口上的后关联操作[ *Dot11ExtIhvPerformPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547492)函数。

**请注意**  For Windows Vista 中，只有在基础结构的基本服务设置 (BSS) 网络 IHV 扩展 DLL 支持。

 

执行后关联操作时，IHV 扩展 DLL 可以执行以下操作：

-   分配新的数据端口所需的任何资源。

-   执行专用安全处理对于数据端口，包括发送和接收数据包在预关联操作过程中配置的身份验证算法。 有关此操作的详细信息，请参阅[预关联操作](pre-association-operations.md)。

-   派生密码密钥并将它们下载到 WLAN 适配器。

操作系统将 WLAN 适配器完成同 ap 解除关联操作，通过调用来终止数据端口上的后关联操作[ *Dot11ExtIhvStopPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547521)函数。 此调用，以下操作系统中删除关联的数据端口。

以下主题介绍 IHV 扩展 DLL 必须做什么来执行或停止后关联的操作。

[执行后关联操作](performing-a-post-association-operation.md)

[停止后关联操作](stopping-a-post-association-operation.md)

[接口的本机 802.11 802.1 X 模块](interface-to-the-native-802-11-802-1x-module.md)

有关关联操作的详细信息，请参阅[关联操作](association-operations.md)。

有关解除关联操作的详细信息，请参阅[解除关联操作](disassociation-operations.md)。

有关端口管理中涉及的过程的详细信息，请参阅[基于端口的网络访问](port-based-network-access.md)。

 

 





