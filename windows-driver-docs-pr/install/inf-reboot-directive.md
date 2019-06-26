---
title: INF Reboot 指令
description: 重新启动指令指示应通知调用方以完成安装后重新启动系统。
ms.assetid: 0E2640EA-921D-4677-82EF-EF9707254E66
keywords:
- INF 重启指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF Reboot Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2ad3ad61e5b4bcf5b610a29d01de988ded3b071
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370038"
---
# <a name="inf-reboot-directive"></a>INF Reboot 指令

一个**重新启动**指令指示应通知调用方以完成安装后重新启动系统。

```ini
[DDInstall]
  
Reboot
```

**警告**  **重新启动**中直接指定时，只处理指令 **\[DDInstall\]** 部分。

 

**重新启动**因为需要重新启动系统将自动检测到基于设备的一部分遇到的常见条件对于安装在 Windows 上的 INF 文件几乎永远不会指定指令安装。 例如，系统会通知调用方如果某些目标的目标文件的文件复制操作是在使用中，或者如果设备无法自动重新启动安装过程，则需要重新启动。 **重新启动**为其重新启动系统始终是必需的系统本身不能自动检测此驱动程序安装后某些特定条件时，应仅使用指令。

指定重新启动指令，则调用方将收到通知的系统重启所需的任何设备使用本节 INF 安装的安装。 安装已发起时通过函数的指针等[ **UpdateDriverForPlugAndPlayDevices**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)， [ **DiInstallDriver** ](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldrivera)，或[ **DiInstallDevice**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldevice)，这将导致*NeedReboot* out 参数设置为 TRUE 这些例程。

<a name="remarks"></a>备注
-------

在 Windows 7 及更早版本，使用的设备驱动程序和安装**重新启动**指令将始终导致调用方被通知的系统重启完成安装所必需的。

在 Windows 8 和更高，以上描述的行为仅时发生一个或多个要安装的设备尚未启动。 而不是新的驱动程序在安装期间重启设备，系统将通知调用方的系统重启已完成的新的驱动程序安装所必需的。 如果当前未启动要安装的设备，系统将尝试执行安装，无需重新启动系统。 请注意是否某项操作的安装仍要求仍可能需要重新启动。 例如，如果当前正在使用某些文件要复制的目标文件位置，重新启动系统仍需要以完成安装。

 

 





