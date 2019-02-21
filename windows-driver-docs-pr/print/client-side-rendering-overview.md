---
title: 客户端呈现概述
description: 客户端呈现概述
ms.assetid: 0c73ca03-0fde-423d-80c9-6800468176b5
keywords:
- 有关客户端呈现客户端呈现 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4d6a184876e8b888f1858728047276bae4ce8e7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522696"
---
# <a name="client-side-rendering-overview"></a>客户端呈现概述

[指向并打印](introduction-to-point-and-print.md)加载到与以前版本的 Windows 操作系统的客户端计算机上的打印机驱动程序。 客户端呈现导致打印机驱动程序来呈现打印机的增强型图元文件 (EMF) 格式或打印机驱动程序使用的 XML 纸张规范 (XPS) 格式使用而不是页面描述语言 (PDL) 到的打印作业。 然后将 RAW 格式 PDL 发送到打印服务器的队列和打印的打印后台处理程序中的新功能。

除将打印作业呈现的处理负载从打印服务器移动到客户端计算机，客户端呈现还向用户提供以下优势：

-   消除了驱动程序不匹配问题。

    后台处理打印作业在同一台计算机还会呈现的 EMF 格式数据，因为不再有问题在客户端有与打印服务器上的版本不兼容的打印机驱动程序版本。

-   支持脱机打印。

    最终用户可以现在后台打印到远程打印机的打印作业，即使它们未连接到承载打印机的打印服务器。 客户端呈现功能，使用户可以后台处理和呈现本地打印作业。 当客户端计算机可以建立到打印后台处理程序的连接时，呈现打印作业是自动发送到打印服务器进行打印。
