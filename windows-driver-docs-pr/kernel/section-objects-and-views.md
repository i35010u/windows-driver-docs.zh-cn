---
title: 节对象和视图
description: 节对象和视图
ms.assetid: 9c60b761-6326-4d1a-b884-cc2acee4bedd
keywords:
- 内存管理 WDK 内核，部分对象
- 内存管理 WDK 内核，共享内存
- 共享的内存 WDK 内核
- 部分对象 WDK 内核
- 内存部分 WDK 内核
- 共享内存地址空间
- 视图 WDK 内存部分
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 215aa48e7af3a94377b7e775da1e21ba47bd61f4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377296"
---
# <a name="section-objects-and-views"></a>节对象和视图





一个*节对象*表示一段的可共享的内存。 一个进程可以使用的部分对象与其他进程共享的内存地址空间 （内存的部分） 的部分。 部分对象还提供的过程可以将文件映射到其内存地址空间的机制。

每个内存部分都有一个或多个相应*视图*。 节的视图是包含到的进程可见部分。 创建一个视图的一个部分通常所说的操作*映射*部分中的视图。 操作的部分内容的每个进程具有其自己的视图;一个进程还可以 （到相同或不同节中） 有多个视图。

本部分包含以下主题：

[文件备份和支持页的文件部分](file-backed-and-page-file-backed-sections.md)

[管理内存部分](managing-memory-sections.md)

[部分对象和视图的安全问题](security-issues-for-section-objects-and-views.md)

 

 




