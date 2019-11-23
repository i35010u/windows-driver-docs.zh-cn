---
title: 对象管理器支持例程
description: 对象管理器支持例程
ms.assetid: 64dc1cfb-faf6-4fe0-a8d9-99f6da6d59b7
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: 3ff5f70d40fc756b179073985c24fe2a5e2f7132
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955819"
---
# <a name="object-manager-support-routines"></a>对象管理器支持例程

下表列出了系统提供的对象管理支持例程的子集，这些例程可由内核模式文件系统和文件系统（微筛选器和旧版）筛选器驱动程序使用，并保留供系统使用。 设备驱动程序无法使用这些例程。

除了此处所述的例程，文件系统和文件系统筛选器驱动程序还可以调用内核模式驱动程序体系结构引用中描述的任何**Ob**_Xxx_例程，并在*ntifs*中声明。

**头文件：** *ntifs*

**前缀： Ob**_Xxx_

| 函数或宏 | 描述 |
| ----------------- | ----------- |
| **ObInsertObject** | 保留供系统使用。 |
| **ObIsKernelHandle** | 确定指定的句柄是否为内核句柄。 |
| **ObMakeTemporaryObject** | 保留供系统使用。 |
| **ObOpenObjectByPointer** | 打开由指针引用的对象，并返回该对象的句柄。 |
| **ObQueryNameString** | 提供调用方具有其指针的给定对象的名称（如果有）。 |
| **ObQueryObjectAuditingByHandle** | 保留供系统使用。 |
