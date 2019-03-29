---
title: 使用 PnP 通知
description: 使用 PnP 通知
ms.assetid: cc6c9106-37b3-473c-bbd2-89701d698fdf
keywords:
- WDK 即插即用通知
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93a866b086294e479ca227688f5ca751119950aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568974"
---
# <a name="using-pnp-notification"></a>使用 PnP 通知





即插即用的环境中，在驱动程序和应用程序需要在计算机上对设备的配置中的更改做出反应。 例如，应用程序需要知道时已添加到计算机所需的设备和驱动程序需要知道特定设备上发生更改时。

PnP 管理器提供了一种机制，用于驱动程序和应用程序特定的即插即用事件发生时接收通知。 本部分介绍如何在内核模式代码中使用即插即用通知。 用户模式应用程序的编写器应看到的信息的 Microsoft Windows SDK 文档**RegisterDeviceNotification**函数和相关的函数。

 

 




