---
title: SCSI 微型端口驱动程序
description: SCSI 微型端口驱动程序
ms.assetid: d9268be8-a68d-4617-b323-349ce7c62f3f
keywords:
- SCSI 微型端口驱动程序 WDK 存储
- 存储微型端口驱动程序 WDK，SCSI 微型端口驱动程序
- 微型端口驱动程序 WDK 存储，SCSI 微型端口驱动程序
- SCSI 微型端口驱动程序 WDK 存储，关于 SCSI 微型端口驱动程序
- HBA WDK SCSI
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0961a052c3b8273459992e95214f85e955c923b0
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252453"
---
# <a name="scsi-miniport-drivers"></a>SCSI 微型端口驱动程序

本部分包含以下信息：

[支持 SCSI 微型端口驱动程序中的即插即用](supporting-plug-and-play-in-a-scsi-miniport-driver.md)

[即插即用 SCSI 微型端口驱动程序的注册表项](registry-entries-for-plug-and-play-scsi-miniport-drivers.md)

[对用于管理启动驱动器的 SCSI 微型端口驱动程序的限制](restrictions-on-scsi-miniport-drivers-that-manage-the-boot-drive.md)

[SCSI 微型端口驱动程序中的错误处理](error-handling-in-scsi-miniport-drivers.md)

[SCSI 微型端口驱动程序例程](scsi-miniport-driver-routines.md)

基于 NT 的操作系统的 SCSI 微型端口驱动程序是特定于 HBA 但独立于操作系统的驱动程序。 也就是说，每个微型端口驱动程序将自身与系统提供的 SCSI 端口驱动程序链接在一起，这是一个动态链接库（DLL），只调用端口驱动程序的 **ScsiPort * * * Xxx*例程来与系统及其 HBA 通信。 此类 SCSI 微型端口驱动程序在其他支持 Microsoft Win32 应用程序的 Microsoft 操作系统上运行，同时导出 **ScsiPort * * * Xxx*例程。 有关 **ScsiPort * * Xxx*例程的详细信息，请参阅[SCSI 端口驱动程序支持例程](scsi-port-driver-support-routines.md)。

请注意，除 **ScsiPort * * * Xxx*之外的任何调用例程的 SCSI 微型端口驱动程序都无法在这两个 Microsoft 操作系统环境中运行。 若要跨 Microsoft Windows 系统（包括基于 NT 的操作系统）保持便携式，SCSI 微型端口驱动程序必须仅调用系统提供的 **ScsiPort * * * Xxx*。

SCSI 微型端口驱动程序可以是即插即用的驱动程序，也可以作为不参与即插即用操作（如资源重新分发或电源管理）的旧驱动程序运行。 即插即用和旧微型端口驱动程序之间的主要区别是调用初始化例程的顺序，并强制实施在 Microsoft Windows NT 4.0 中应用于微型端口驱动程序但不强制执行的某些限制。
