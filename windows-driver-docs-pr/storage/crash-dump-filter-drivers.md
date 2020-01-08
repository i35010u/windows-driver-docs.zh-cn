---
title: 故障转储筛选器驱动程序简介
description: 故障转储筛选器驱动程序
ms.assetid: d91c00d7-ad17-4fa8-9e78-fee0698d9049
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 51795c1f0025a6f87a5933b0826c770fe40786c1
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606441"
---
# <a name="introduction-to-crash-dump-filter-drivers"></a>故障转储筛选器驱动程序简介

为了扩展故障转储接口的有用性，对于带有 Service Pack 1 （SP1）的 Windows Vista 和 Windows Server 2008 及更高版本的操作系统，Microsoft 已在崩溃转储驱动程序堆栈中定义筛选器驱动程序支持。

故障转储驱动程序不使用典型的运行时存储驱动程序堆栈将转储数据写入磁盘。 通过在崩溃转储驱动程序堆栈中添加筛选器驱动程序支持，可以在不更改内核的情况下添加新功能。 例如，可以加密休眠或故障转储文件的内容。
