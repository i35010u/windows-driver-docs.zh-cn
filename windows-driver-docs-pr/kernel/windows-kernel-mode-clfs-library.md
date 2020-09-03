---
title: Windows 内核模式 CLFS 库
description: Windows 内核模式 CLFS 库
ms.assetid: 4da3cb49-dc20-4713-813b-ff458c99ab90
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d617c232b3ab26c409f4a59f1d95f4adde64adca
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403496"
---
# <a name="windows-kernel-mode-clfs-library"></a>Windows 内核模式 CLFS 库


Windows 为系统文件提供了事务日志记录系统。 此系统称为公用日志文件系统 (CLFS) 。 有关 CLFS 的详细信息，请参阅 [公用日志文件系统](introduction-to-the-common-log-file-system.md)。

为 CLFS 提供直接接口的例程的前缀为 "**CLFS**";有关 CLFS 库例程的列表，请参阅 [公用日志文件系统 (CLFS) 库例程](/windows-hardware/drivers/ddi/index)。 CLFS 还提供了一个例程列表，你可以实现这些例程来管理 CLFS;有关 CLFS 管理的详细信息，请参阅 [CLFS 管理库例程](/windows-hardware/drivers/ddi/index)。

CLFS 是一种与事务文件系统相关的技术;有关事务的详细信息，请参阅 [Windows 内核模式事务管理器](windows-kernel-mode-kernel-transaction-manager.md)。

 

