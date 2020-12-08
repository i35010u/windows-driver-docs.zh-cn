---
title: 故障转储筛选器驱动程序简介
description: 故障转储筛选器驱动程序
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: c250ec04ec5d259146d0202f7b92b78473b4ed88
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804709"
---
# <a name="introduction-to-crash-dump-filter-drivers"></a>故障转储筛选器驱动程序简介

为了扩展故障转储接口的有用性，对于带有 Service Pack 1 (SP1) 和 Windows Server 2008 及更高版本操作系统的 Windows Vista，Microsoft 已在崩溃转储驱动程序堆栈中定义筛选器驱动程序支持。

故障转储驱动程序不使用典型的运行时存储驱动程序堆栈将转储数据写入磁盘。 通过在崩溃转储驱动程序堆栈中添加筛选器驱动程序支持，可以在不更改内核的情况下添加新功能。 例如，可以加密休眠或故障转储文件的内容。
