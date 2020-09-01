---
title: INF Reboot 指令
description: 重新启动指令表明在安装完成后应通知调用方重新启动系统。
ms.assetid: 0E2640EA-921D-4677-82EF-EF9707254E66
keywords:
- INF 重新启动指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF Reboot Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae7aa1b5fe5dfda83ec7d8dc45675866aac238cb
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097299"
---
# <a name="inf-reboot-directive"></a>INF Reboot 指令

**重新启动**指令表明在安装完成后应通知调用方重新启动系统。

```inf
[DDInstall]
  
Reboot
```

**警告**   仅当在** \[ \] DDInstall**节中直接指定时才处理**Reboot**指令。

 

在 INF 文件中，在 Windows 上的安装过程中几乎从未指定 **reboot** 指令，因为系统会根据在设备安装过程中遇到的常见情况，自动检测重新启动系统的需求。 例如，如果文件复制操作的某个目标目标文件正在使用中，或者如果在安装过程中无法自动重新启动设备，则系统将通知调用方需要重新启动。 只有在安装了此驱动程序之后，系统本身无法自动检测到某些特定条件时，才应使用 **reboot** 指令。

指定 reboot 指令后，将通知调用方系统需要重新启动系统才能完成使用此 INF 安装部分的任何设备的安装。 当通过 [**UpdateDriverForPlugAndPlayDevices**](/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)、 [**DiInstallDriver**](/windows/desktop/api/newdev/nf-newdev-diinstalldrivera)或 [**DiInstallDevice**](/windows/desktop/api/newdev/nf-newdev-diinstalldevice)等函数启动安装时，这将导致这些例程的 *NeedReboot* out 参数设置为 TRUE。

<a name="remarks"></a>备注
-------

在 Windows 7 和更早版本上，使用带有 **重新启动** 指令的驱动程序安装设备将始终导致调用方通知系统需要重新启动系统才能完成安装。

在 Windows 8 及更高版本上，仅当已经启动了一个或多个要安装的设备时，才会出现上述行为。 系统不会在安装新驱动程序的过程中重新启动设备，而是通知调用方需要重新启动系统才能完成新驱动程序的安装。 如果要安装的设备当前未启动，则系统将尝试执行安装，而无需重新启动系统。 请注意，如果安装操作之一仍需要重新启动，则可能仍需要重新启动。 例如，如果要复制的某个文件的目标文件位置当前正在使用中，则仍需要重新启动系统才能完成安装。

 

