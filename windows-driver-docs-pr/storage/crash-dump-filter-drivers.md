---
title: 故障转储筛选器驱动程序
description: 故障转储筛选器驱动程序
ms.assetid: d91c00d7-ad17-4fa8-9e78-fee0698d9049
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec7da19c64f38f62230b51bb7e808ecbee00ce1f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345203"
---
# <a name="crash-dump-filter-drivers"></a>故障转储筛选器驱动程序


若要扩展的 Windows Vista Service Pack 1 (SP1) 和 Windows Server 2008 和更高版本操作系统的崩溃转储接口，用途，Microsoft 已崩溃转储驱动程序堆栈中定义筛选器驱动程序支持。

崩溃转储驱动程序不使用典型的运行时存储驱动程序堆栈转储数据写入磁盘。 通过崩溃转储驱动程序堆栈中添加筛选器驱动程序支持，而无需更改内核可以添加新功能。 例如，就能够对休眠或崩溃转储文件的内容进行加密。

 

 




