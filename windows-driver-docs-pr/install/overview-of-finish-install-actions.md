---
title: 完成安装操作概述
description: 完成安装操作概述
ms.assetid: 986ac884-2970-4eda-a800-88fd30b95562
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0ea4716a90be11cc970705621d0ab19ff65b682
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547463"
---
# <a name="overview-of-finish-install-actions"></a>完成安装操作概述


如果*安装程序*（安装程序类、 类共同安装程序中或设备共同安装程序） 提供了完成安装操作的设备，Windows 运行完成安装操作*后*所有其他设备设备的安装操作已完成，并启动设备。 在新系统上，完成安装操作运行第一次完成 Windows 后启动操作系统。

设备安装操作包括：

-   *核心设备安装*(也称为*服务器端安装*)，在设备的驱动程序安装在受信任的系统上下文中并无需用户交互。

Windows 进程*完成安装操作*而不考虑是否通过将插设备连接到计算机中启动安装时相同的方式 ( [*硬件第一个安装*](hardware-first-installation.md)) 或通过运行如发现新硬件向导、 更新驱动程序软件向导或供应商提供的安装程序的安装程序启动安装 (*软件第一个安装*).

Windows 仅在具有管理员权限的用户的上下文中运行完成安装操作。

从 Windows Vista 开始，用户帐户控制 (UAC)，用户可以在更低时运行权限; 大多数情况下，和提升权限仅在必要时。 因此，如果调用在完成安装过程，Windows 会提示用户同意的情况下以及运行完成安装操作所需的凭据。 如果用户不提供同意或提供所需的凭据，完成安装操作都推迟到确实能够提供同意和所需的凭据的用户登录。

**请注意**  如果 UAC 设置为默认设置 （仅当时通知我程序尝试更改我的计算机） 或较低的设置，从 Windows 7 开始，操作系统不显示与管理用户的提示当处理完成安装操作的权限。

 

 

 





