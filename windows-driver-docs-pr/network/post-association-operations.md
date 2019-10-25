---
title: “关联后的操作”概述
description: “关联后的操作”概述
ms.assetid: e4c7ea7a-53ad-41b2-bf3f-03c770e58043
keywords:
- IHV 扩展 DLL WDK 本机802.11，后关联操作
- 后关联操作 WDK 本机 802.11 IHV 扩展 DLL
- 本机 802.11 IHV 扩展 DLL WDK，后关联操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a670e81fdffa71b3dcd61d5366a96b47d8faf9c6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843684"
---
# <a name="post-association-operations-overview"></a>“关联后的操作”概述

当无线 LAN （WLAN）适配器成功完成与访问点（AP）的关联操作时，操作系统将为关联创建数据端口。 然后，操作系统通过调用[*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)函数在数据端口上启动关联后操作。

**注意**  对于 Windows VISTA，IHV 扩展 DLL 仅支持基础结构基本服务集（BSS）网络。

 

执行后关联操作时，IHV 扩展 DLL 可以执行以下操作：

-   为新的数据端口分配所需的任何资源。

-   对数据端口执行专有安全处理，包括在预关联操作期间为配置的身份验证算法发送和接收数据包。 有关此操作的详细信息，请参阅[预关联操作](pre-association-operations.md)。

-   派生密码密钥并将其下载到 WLAN 适配器。

当 WLAN 适配器使用 AP 完成解除关联的操作时，操作系统将通过调用[*Dot11ExtIhvStopPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)函数终止对数据端口的关联后操作。 执行此调用后，操作系统将删除关联的数据端口。

以下主题介绍了在执行或停止关联后操作时，IHV 扩展 DLL 必须执行的操作。

[执行后关联操作](performing-a-post-association-operation.md)

[停止关联后操作](stopping-a-post-association-operation.md)

[本机 802.11 802.1 X 模块的接口](interface-to-the-native-802-11-802-1x-module.md)

有关关联操作的详细信息，请参阅[关联运算](association-operations.md)。

有关解除相关操作的详细信息，请参阅解除相关[操作](disassociation-operations.md)。

有关端口管理中涉及的过程的详细信息，请参阅[基于端口的网络访问](port-based-network-access.md)。

 

 





