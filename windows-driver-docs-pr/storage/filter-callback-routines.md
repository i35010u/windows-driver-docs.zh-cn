---
title: 筛选器回调例程
description: 筛选器回调例程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ac23c7d8620fa6630ee0bec183eb1c0808b4752
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835301"
---
# <a name="filter-callback-routines"></a>筛选器回调例程


故障转储驱动程序在崩溃转储筛选器驱动程序中支持以下回调例程。 这些回调例程并不是必需的，因此，故障转储筛选器驱动程序可以自由地仅实现添加所需功能所需的回调例程。

[**转储 \_ 启动**](/windows-hardware/drivers/ddi/ntdddump/nc-ntdddump-dump_start)

[**转储 \_ 写入**](/windows-hardware/drivers/ddi/ntdddump/nc-ntdddump-dump_write)

[**转储 \_ 读取**](/windows-hardware/drivers/ddi/ntdddump/nc-ntdddump-dump_read)

[**转储 \_ 完成**](/windows-hardware/drivers/ddi/ntdddump/nc-ntdddump-dump_finish)

[**转储 \_ 卸载**](/windows-hardware/drivers/ddi/ntdddump/nc-ntdddump-dump_unload)

 

