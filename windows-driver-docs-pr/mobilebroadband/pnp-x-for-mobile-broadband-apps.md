---
title: 适合移动宽带应用的 PnP-X
description: 适合移动宽带应用的 PnP-X
ms.assetid: f8f4756e-00b6-4778-9d67-73653865cf54
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1da63bdd09fc636268767eb18ae53717211ea40
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210809"
---
# <a name="pnp-x-for-mobile-broadband-apps"></a>适合移动宽带应用的 PnP-X


## <a name="span-idapp_installationspanspan-idapp_installationspanspan-idapp_installationspanapp-installation"></a><span id="App_installation"></span><span id="app_installation"></span><span id="APP_INSTALLATION"></span>应用安装


移动宽带适配器使用户有机会在连接适配器时，自动安装相应的移动宽带应用。 个人热点无法从同一基于 SIM 的载波检测中获益。 但是，实现 Pnp-x 协议的个人热点可以选择要安装的应用。 当计算机对 Pnp-x 设备进行配对时，会自动安装该应用。

这可以是自动为移动宽带用户自动安装的应用，也可以是设备制造商和操作员创作的品牌应用。 应用应包含与标准移动宽带应用相同的许多功能。 有关移动宽带应用中的标准体验建议，请参阅 [设计移动宽带应用的用户体验](designing-the-user-experience-of-a-mobile-broadband-app.md) 。

某些类的网络设备将自动配对;有关详细信息，请参阅 [内部设备的 UWP 设备应用](../devapps/uwp-device-apps-for-specialized-devices.md)。 其他设备类在用户通过使用计算机设置与设备配对之前，不会自动安装应用程序。

## <a name="span-idapp_privilegesspanspan-idapp_privilegesspanspan-idapp_privilegesspanapp-privileges"></a><span id="App_privileges"></span><span id="app_privileges"></span><span id="APP_PRIVILEGES"></span>应用特权


尽管应用程序无法访问与移动宽带应用相同的特权 Api，但它可以通过网络与设备进行通信，以便在设备公开此信息时检索等效的信息。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[通信通道](communication-channels.md)

 

