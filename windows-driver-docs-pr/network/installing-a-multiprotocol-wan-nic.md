---
title: 安装多协议 WAN NIC
description: 安装多协议 WAN NIC
ms.assetid: 7000040c-8a26-496d-ae26-580aace68160
keywords:
- 添加注册表部分 WDK 网络、 多协议 WAN NIC
- 多协议 WAN NIC WDK 网络
- WAN NIC WDK 网络
- NIC 多协议 WAN WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e1bda00517265c5d9fd04c9b27608d59abbfaaf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385850"
---
# <a name="installing-a-multiprotocol-wan-nic"></a>安装多协议 WAN NIC





多协议的 WAN NIC 提供了多个 WAN 协议。 例如，此类 NIC 可能允许用户选择 ISDN，帧中继或信道化 T1。 用户在配置 NIC 时的 nic 或安装期间选择的 WAN 协议

> [!NOTE]
> ISDN 功能已被弃用，在 Windows 10 及更高版本。 


多协议的 WAN NIC 的供应商必须提供的共同安装程序安装向导页。 (有关共同安装程序的详细信息，请参阅[编写共同安装程序](https://docs.microsoft.com/windows-hardware/drivers/install/writing-a-co-installer))。 此向导页会提示用户选择 WAN 协议：

-   如果用户选择 ISDN，将显示 ISDN 向导。 ISDN 向导会提示用户为 ISDN 交换机类型，并根据选择的交换机类型，其他 ISDN 参数值。 有关详细信息，请参阅[指定 ISDN 键和值的 ISDN 适配器](specifying-isdn-keys-and-values-for-an-isdn-adapter.md)。

-   如果用户可以选择除 ISDN 之外的 WAN 协议，该向导将添加**ShowIsdnPages**与 WAN NIC 的实例键的注册表值。 该向导，在这种情况下，设置**ShowIsdnPages**为零，以禁止 ISDN 向导显示。 只要**ShowIsdnPages**为零，抑制 ISDN 向导。

安装 WAN NIC 后，用户可以重新配置的 NIC，使用 NIC 的属性页：

-   如果用户将更改协议从 ISDN 到另一种 WAN 协议，属性页将添加**ShowIsdnPages** WAN NIC 实例注册表项，如有必要的注册表值。 属性页集**ShowIsdnPages**为零，以禁止 ISDN 向导显示。

-   如果用户将协议更改为 ISDN，WAN NIC 的属性页将显示一个对话框，提示用户以应用更改。 当用户应用更改时，属性页用于设置**ShowIsdnPages**为 1。 当用户再次打开 NIC 的属性页时，将显示 ISDN 向导。

请注意， **LowerRange**多协议的 WAN nic 支持 ISDN 绑定接口必须设置为**isdn**。 有关详细信息，请参阅[指定绑定接口](specifying-binding-interfaces.md)。 如果**ShowIsdnPages**注册表值不存在，如果 NIC **LowerRange**设置为**isdn**，ISDN 向导将显示在安装和配置过程nic。 如果**ShowIsdnPages**设置为零，则不显示 ISDN 向导。 如果**ShowIsdnPages**设置为 1，在 NIC 配置期间显示 ISDN 向导

 

 





