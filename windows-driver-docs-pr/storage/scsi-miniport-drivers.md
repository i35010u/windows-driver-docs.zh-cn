---
title: SCSI 微型端口驱动程序
description: SCSI 微型端口驱动程序
ms.assetid: d9268be8-a68d-4617-b323-349ce7c62f3f
keywords:
- SCSI 微型端口驱动程序 WDK 存储
- 存储微型端口驱动程序 WDK、 SCSI 微型端口驱动程序
- 微型端口驱动程序 WDK 存储，SCSI 微型端口驱动程序
- SCSI 微型端口驱动程序 WDK 存储，有关 SCSI 微型端口驱动程序
- HBA WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 213dcbeda8bb27f283cea1c46d84ae54ea7f30a6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386490"
---
# <a name="scsi-miniport-drivers"></a>SCSI 微型端口驱动程序


## <span id="ddk_scsi_miniport_drivers_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_KG"></span>


本部分包含以下信息：

[支持即插在 SCSI 微型端口驱动程序](supporting-plug-and-play-in-a-scsi-miniport-driver.md)

[Plug and Play SCSI 微型端口驱动程序的注册表项](registry-entries-for-plug-and-play-scsi-miniport-drivers.md)

[管理启动驱动器的 SCSI 微型端口驱动程序的限制](restrictions-on-scsi-miniport-drivers-that-manage-the-boot-drive.md)

[SCSI 微型端口驱动程序中的错误处理](error-handling-in-scsi-miniport-drivers.md)

[必需和可选 SCSI 微型端口驱动程序例程](required-and-optional-scsi-miniport-driver-routines.md)

基于 NT 的操作系统的 SCSI 微型端口驱动程序特定于 HBA 的但独立于操作系统的。 每个微型端口驱动程序，即使用系统提供 SCSI 端口驱动程序，它是一个动态链接库 (DLL)，并调用仅端口驱动程序的链接本身 **ScsiPort * * * Xxx*例程与系统和其 HBA 进行通信。 此类 SCSI 微型端口驱动程序运行其他 Microsoft 操作系统上支持 Microsoft Win32 应用程序，还将导出 **ScsiPort * * * Xxx*例程。 有关详细信息 **ScsiPort * * * Xxx*例程，请参阅[SCSI 端口库例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

请注意，任何 SCSI 微型端口驱动程序的调用例程以外 **ScsiPort * * * Xxx*无法在这两个 Microsoft 操作系统环境中运行。 若要跨多个 Microsoft Windows 系统，包括基于 NT 的操作系统，保持可移植 SCSI 微型端口驱动程序必须调用仅系统提供 **ScsiPort * * * Xxx*。

SCSI 微型端口驱动程序可以插驱动程序，也可以作为不参与插操作，如资源重新分发或电源管理的旧驱动程序运行。 Plug and Play 和旧的微型端口驱动程序之间的主要区别是在调用的初始化例程和强制执行的某些限制已应用于 Microsoft Windows NT 4.0 中的微型端口驱动程序但不是会强制执行的顺序。

 

 




