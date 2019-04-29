---
title: 下载驱动程序特定的文件
description: 下载驱动程序特定的文件
ms.assetid: 7ac5057a-32fb-4c3a-a5c3-3fc1217dbdc6
keywords:
- 点和打印 WDK，特定于驱动程序的文件
- 特定于驱动程序文件 WDK 打印机
- 下载特定于驱动程序的打印机文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7f3d7547808e0af7b06a1b297561f796f0fcc92
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387269"
---
# <a name="downloading-driver-specific-files"></a>下载驱动程序特定的文件





客户端系统创建到打印服务器的连接通过调用**AddPrinterConnection**。 此调用会导致调用**GetPrinterDriver**的服务器上，其中读取[打印机的 INF 文件](printer-inf-files.md)为了填充到驱动程序\_信息\_3 结构，然后通过调用**AddPrinterDriver**，使用驱动程序\_信息\_3 结构作为输入。 **AddPrinterDriver**函数会导致驱动程序中列出的所有文件\_信息\_3 结构要发送到客户端。

这些函数和驱动程序\_信息\_3 结构 Microsoft Windows SDK 文档中所述。

 

 




