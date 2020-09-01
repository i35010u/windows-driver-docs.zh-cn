---
title: 筛选器回调例程
description: 筛选器回调例程
ms.assetid: 3d9f874c-f026-40fc-a97d-0d4cefa3d1f9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b19b79dbed82d55069473c36ba58d608d9de195
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186894"
---
# <a name="filter-callback-routines"></a>筛选器回调例程


故障转储驱动程序在崩溃转储筛选器驱动程序中支持以下回调例程。 这些回调例程并不是必需的，因此，故障转储筛选器驱动程序可以自由地仅实现添加所需功能所需的回调例程。

[**转储 \_ 启动**](/windows-hardware/drivers/ddi/ntdddump/nc-ntdddump-dump_start)

[**转储 \_ 写入**](/windows-hardware/drivers/ddi/ntdddump/nc-ntdddump-dump_write)

[**转储 \_ 读取**](/windows-hardware/drivers/ddi/ntdddump/nc-ntdddump-dump_read)

[**转储 \_ 完成**](/windows-hardware/drivers/ddi/ntdddump/nc-ntdddump-dump_finish)

[**转储 \_ 卸载**](/windows-hardware/drivers/ddi/ntdddump/nc-ntdddump-dump_unload)

 

