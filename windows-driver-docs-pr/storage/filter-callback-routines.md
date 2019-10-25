---
title: 筛选器回调例程
description: 筛选器回调例程
ms.assetid: 3d9f874c-f026-40fc-a97d-0d4cefa3d1f9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3552afba819c6a39e7905f4ffe833ab75bd61a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844838"
---
# <a name="filter-callback-routines"></a>筛选器回调例程


故障转储驱动程序在崩溃转储筛选器驱动程序中支持以下回调例程。 这些回调例程并不是必需的，因此，故障转储筛选器驱动程序可以自由地仅实现添加所需功能所需的回调例程。

[**转储\_开始**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdddump/nc-ntdddump-dump_start)

[**写入\_转储**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdddump/nc-ntdddump-dump_write)

[**转储\_读取**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdddump/nc-ntdddump-dump_read)

[**转储\_完成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdddump/nc-ntdddump-dump_finish)

[**转储\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdddump/nc-ntdddump-dump_unload)

 

 




