---
title: Windows 内核模式 CLFS 库
description: Windows 内核模式 CLFS 库
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ec9cdf07b427dbf6c6a084bb91fda6f95a7a9529
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814213"
---
# <a name="windows-kernel-mode-clfs-library"></a>Windows 内核模式 CLFS 库


Windows 为系统文件提供了事务日志记录系统。 此系统称为公用日志文件系统 (CLFS) 。 有关 CLFS 的详细信息，请参阅 [公用日志文件系统](introduction-to-the-common-log-file-system.md)。

为 CLFS 提供直接接口的例程的前缀为 "**CLFS**";有关 CLFS 库例程的列表，请参阅 [公用日志文件系统 (CLFS) 库例程](/windows-hardware/drivers/ddi/index)。 CLFS 还提供了一个例程列表，你可以实现这些例程来管理 CLFS;有关 CLFS 管理的详细信息，请参阅 [CLFS 管理库例程](/windows-hardware/drivers/ddi/index)。

CLFS 是一种与事务文件系统相关的技术;有关事务的详细信息，请参阅 [Windows Kernel-Mode 事务管理器](windows-kernel-mode-kernel-transaction-manager.md)。

 

