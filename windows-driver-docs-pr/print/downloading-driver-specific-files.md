---
title: 下载驱动程序特定的文件
description: 下载驱动程序特定的文件
keywords:
- 指向和打印 WDK，特定于驱动程序的文件
- 特定于驱动程序的文件 WDK 打印机
- 下载驱动程序特定的打印机文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9590b74847757de9dfde425ed4bf910c644c4659
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797197"
---
# <a name="downloading-driver-specific-files"></a>下载驱动程序特定的文件





客户端系统通过调用 **AddPrinterConnection** 创建到打印服务器的连接。 此调用会导致在服务器上调用 **GetPrinterDriver** ，这会读取 [打印机的 INF 文件](printer-inf-files.md) ，以填充驱动程序 \_ 信息 \_ 3 结构，然后调用 **AddPrinterDriver**，并将驱动程序 \_ info \_ 3 结构作为输入。 **AddPrinterDriver** 函数将导致驱动程序 INFO 3 结构中列出的所有文件 \_ \_ 都发送到客户端。

\_Microsoft Windows SDK 文档中介绍了这些函数和驱动程序信息 \_ 3 的结构。

 

 




