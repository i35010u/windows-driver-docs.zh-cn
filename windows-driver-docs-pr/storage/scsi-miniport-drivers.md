---
title: SCSI 微型端口驱动程序
description: SCSI 微型端口驱动程序
keywords:
- SCSI 微型端口驱动程序 WDK 存储
- 存储微型端口驱动程序 WDK，SCSI 微型端口驱动程序
- 微型端口驱动程序 WDK 存储，SCSI 微型端口驱动程序
- SCSI 微型端口驱动程序 WDK 存储，关于 SCSI 微型端口驱动程序
- HBA WDK SCSI
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4de507896e4c020a2db4adf9eb0dc3df897f2d95
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836669"
---
# <a name="scsi-miniport-drivers"></a>SCSI 微型端口驱动程序

本部分包含以下信息：

[支持 SCSI 微型端口驱动程序中的即插即用](supporting-plug-and-play-in-a-scsi-miniport-driver.md)

[即插即用 SCSI 微型端口驱动程序的注册表项](registry-entries-for-plug-and-play-scsi-miniport-drivers.md)

[对管理启动驱动器的 SCSI 微型端口驱动程序的限制](restrictions-on-scsi-miniport-drivers-that-manage-the-boot-drive.md)

[SCSI 微型端口驱动程序中的错误处理](error-handling-in-scsi-miniport-drivers.md)

[SCSI 微型端口驱动程序例程](scsi-miniport-driver-routines.md)

基于 NT 的操作系统的 SCSI 微型端口驱动程序是特定于 HBA 但独立于操作系统的驱动程序。 也就是说，每个微型端口驱动程序将自身与系统提供的 SCSI 端口驱动程序链接在一起，该驱动程序是一个动态链接库 (DLL) ，并只调用端口驱动程序的 **ScsiPort**_Xxx_ 例程来与系统及其 HBA 通信。 此类 SCSI 微型端口驱动程序在其他支持 Microsoft Win32 应用程序的 Microsoft 操作系统上运行，并且还导出 **ScsiPort**_Xxx_ 例程。 有关 **ScsiPort**_Xxx_ 例程的详细信息，请参阅 [SCSI 端口驱动程序支持例程](scsi-port-driver-support-routines.md)。

请注意，调用 **ScsiPort**_Xxx_ 以外的例程的任何 SCSI 微型端口驱动程序都无法在这两个 Microsoft 操作系统环境中运行。 若要跨 Microsoft Windows 系统（包括基于 NT 的操作系统）保持便携式，SCSI 微型端口驱动程序必须仅调用系统提供的 **ScsiPort**_Xxx_。

SCSI 微型端口驱动程序可以是即插即用的驱动程序，也可以作为不参与即插即用操作（如资源重新分发或电源管理）的旧驱动程序运行。 即插即用和旧微型端口驱动程序之间的主要区别是调用初始化例程的顺序，并强制实施在 Microsoft Windows NT 4.0 中应用于微型端口驱动程序但不强制执行的某些限制。
