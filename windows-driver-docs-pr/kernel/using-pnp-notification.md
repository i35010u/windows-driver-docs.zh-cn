---
title: 使用 PnP 通知
description: 使用 PnP 通知
keywords:
- 通知 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7afe78c7645795d3de019d4bf1ad9506288d364
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816025"
---
# <a name="using-pnp-notification"></a>使用 PnP 通知





在 PnP 环境中，驱动程序和应用程序需要对计算机上设备配置的更改做出反应。 例如，应用程序需要知道感兴趣的设备何时添加到计算机，驱动程序需要知道何时在特定设备上进行更改。

PnP 管理器提供了一种机制，用于在发生特定 PnP 事件时通知驱动程序和应用程序。 本部分介绍如何在内核模式代码中使用 PnP 通知。 用户模式应用程序的编写器应查看 Microsoft Windows SDK 文档，以获取有关 **RegisterDeviceNotification** 函数和相关函数的信息。

 

 




