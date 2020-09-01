---
title: 安装多协议 WAN NIC
description: 安装多协议 WAN NIC
ms.assetid: 7000040c-8a26-496d-ae26-580aace68160
keywords:
- 添加-注册表-每节 WDK 网络，多协议 WAN NIC
- 多协议 WAN NIC WDK 网络
- WAN NIC WDK 网络
- NIC 多协议 WAN WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52f4667e70979ec64e6f84063757101842641452
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218081"
---
# <a name="installing-a-multiprotocol-wan-nic"></a>安装多协议 WAN NIC





多协议 WAN NIC 提供多种 WAN 协议。 例如，这种 NIC 可能允许用户选择 ISDN、帧中继或 channelized T1。 用户在安装 NIC 或配置 NIC 时选择 WAN 协议。

> [!NOTE]
> 在 Windows 10 及更高版本中，ISDN 功能已弃用。 


多协议 WAN NIC 的供应商必须提供安装向导页的共同安装程序。  (有关共同安装程序的详细信息，请参阅 [编写共同安装程序](../install/writing-a-co-installer.md)) 。 向导页面提示用户选择 WAN 协议：

-   如果用户选择 ISDN，将显示 ISDN 向导。 ISDN 向导会提示用户输入 ISDN 交换机类型和，具体取决于所选交换机类型和其他 ISDN 参数值。 有关详细信息，请参阅为 [Isdn 适配器指定 Isdn 密钥和值](specifying-isdn-keys-and-values-for-an-isdn-adapter.md)。

-   如果用户选择 ISDN 之外的 WAN 协议，则向导会将 **ShowIsdnPages** 注册表值添加到 wan NIC 的实例键。 在这种情况下，该向导将 **ShowIsdnPages** 设置为零，以禁止显示 ISDN 向导。 只要 **ShowIsdnPages** 为零，ISDN 向导就会被取消。

安装 WAN NIC 后，用户可以使用 NIC 的属性页面重新配置 NIC：

-   如果用户将协议从 ISDN 更改为其他 WAN 协议，则在必要时，属性页会将 **ShowIsdnPages** 注册表值添加到 WAN NIC 的实例密钥中。 "属性" 页将 **ShowIsdnPages** 设置为零，以禁止显示 ISDN 向导。

-   如果用户将协议更改为 ISDN，则 WAN NIC 的属性页会显示一个对话框，提示用户应用此更改。 当用户应用更改时，属性页会将 **ShowIsdnPages** 设置为1。 当用户再次打开 NIC 的属性页时，将显示 ISDN 向导。

请注意，支持 ISDN 的多协议 WAN NIC 的 **LowerRange** 绑定接口必须设置为 **isdn**。 有关详细信息，请参阅 [指定绑定接口](specifying-binding-interfaces.md)。 如果 **ShowIsdnPages** 注册表值不存在并且 Nic 的 **LowerRange** 设置为 **isdn**，则会在安装和配置 nic 期间显示 isdn 向导。 如果 **ShowIsdnPages** 设置为零，则不显示 ISDN 向导。 如果 **ShowIsdnPages** 设置为1，则在配置 NIC 期间将显示 ISDN 向导。

 

