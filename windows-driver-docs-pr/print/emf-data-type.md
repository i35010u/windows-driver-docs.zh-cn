---
title: EMF 数据类型
description: EMF 数据类型
ms.assetid: d5a05778-3637-4dba-b036-5f0fc236d52d
keywords:
- 打印处理器 WDK，数据类型
- 数据类型 WDK 打印处理器
- EMF 数据类型 WDK 打印处理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1e49ba1551df5753088de2cdba9463113b0d94e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343195"
---
# <a name="emf-data-type"></a>EMF 数据类型





增强型图元文件 (EMF) 数据包含的指令用于调用 GDI 函数。 打印处理器必须调用 GDI 函数来呈现可打印的图像。 GDI 函数可使打印机驱动程序调用[打印机图形 DLL](printer-graphics-dll.md)，它将图像呈现并将其发送到作为原始数据的后台处理程序 (通过调用[ **EngWritePrinter** ](https://msdn.microsoft.com/library/windows/hardware/ff565467)).

基于 NT 的操作系统的客户端 EMF 将数据发送到基于 NT 的操作系统打印服务器。 EMF 数据与设备无关的并可以比原始数据更快地发送到服务器。 作为 EMF 数据还后台处理打印作业，本地服务器上，由后台后台处理程序线程随后呈现的 EMF 数据时允许向应用程序的快速返回到发出请求的应用程序时。

有关 EMF 数据类型的详细信息，请参阅*Windows 2000 Professional Resource Kit*或*Windows 2000 Server Resource Kit*。 有关增强型图元文件的详细信息，请参阅 Windows SDK 文档。 （这些资源可能不可用在某些语言和国家/地区中。）

 

 




