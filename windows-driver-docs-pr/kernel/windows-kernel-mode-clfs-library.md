---
title: Windows 内核模式 CLFS 库
description: Windows 内核模式 CLFS 库
ms.assetid: 4da3cb49-dc20-4713-813b-ff458c99ab90
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b66a01250770cf0f5644d34b7c53a16e031ece16
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835734"
---
# <a name="windows-kernel-mode-clfs-library"></a>Windows 内核模式 CLFS 库


Windows 为系统文件提供了事务日志记录系统。 此系统称为公用日志文件系统（CLFS）。 有关 CLFS 的详细信息，请参阅[公用日志文件系统](using-common-log-file-system.md)。

为 CLFS 提供直接接口的例程的前缀为 "**CLFS**";有关 CLFS 库例程的列表，请参阅[公用日志文件系统（CLFS）库例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。 CLFS 还提供了一个例程列表，你可以实现这些例程来管理 CLFS;有关 CLFS 管理的详细信息，请参阅[CLFS 管理库例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

CLFS 是一种与事务文件系统相关的技术;有关事务的详细信息，请参阅[Windows 内核模式事务管理器](windows-kernel-mode-kernel-transaction-manager.md)。

 

 




