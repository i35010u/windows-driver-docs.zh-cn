---
title: Finish-Install 操作概述
description: Finish-Install 操作概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98eeda433d24a0ac701956d2c8cc8016698be11a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832653"
---
# <a name="overview-of-finish-install-actions"></a>Finish-Install 操作概述


如果 *安装程序* (类安装程序、类共同安装程序或设备共同安装程序) 提供设备的完成安装操作，则在设备的所有其他设备安装操作完成并且设备已启动 *之后* ，Windows 将运行完成安装操作。 在新系统上，完成安装操作在 Windows 完成后首次启动操作系统。

设备安装操作包括以下各项：

-   *核心设备安装* (也称为 *服务器端安装*) ，其中设备的驱动程序安装在受信任的系统上下文中，无需用户交互。

Windows 处理 "*完成"-安装操作* 的方式相同，无论安装是通过将即插即用设备连接到计算机 (进行 [*硬件首次安装*](hardware-first-installation.md)而启动的) 还是通过运行安装程序（例如 "找到新硬件向导"、"更新驱动程序软件向导" 或供应商提供的安装 (程序）来启动安装 *) 。*

Windows 运行完成-仅在具有管理员权限的用户的上下文中安装操作。

从 Windows Vista 开始，用户帐户控制 (UAC) 使用户能够在大多数时间以较低的特权运行，并且仅在必要时才提升权限。 因此，如果调用了完成安装过程，则 Windows 将提示用户提供许可和运行完成安装操作所需的凭据。 如果用户未提供许可或提供必需的凭据，则会推迟完成安装操作，直到提供同意的用户和所需的凭据登录。

**注意**   从 Windows 7 开始，如果 UAC 设置为默认设置 (仅当程序尝试对我的计算机进行更改时通知我) 或较低的设置时，操作系统将不会在处理完成安装操作时显示具有管理权限的用户的提示。

 

 

 





