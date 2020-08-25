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
ms.openlocfilehash: 8933e9805bbfc84cfe464c13ecd9d3a2f4b21abf
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802771"
---
# <a name="emf-data-type"></a>EMF 数据类型





 (EMF) 数据的增强型图元文件包含调用 GDI 函数的说明。 打印处理器必须调用 GDI 函数以呈现可打印图像。 GDI 函数调用打印机驱动程序的 [打印机图形 DLL](printer-graphics-dll.md)，该 DLL 通过调用 [**EngWritePrinter**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-engwriteprinter)) 来呈现图像，并将其作为原始数据 (发送到后台处理程序。

基于 NT 的操作系统客户端将 EMF 数据发送到基于 NT 的操作系统打印服务器。 EMF 数据独立于设备，并且与原始数据相比，可以更快地发送到服务器。 当请求的应用程序在服务器本地时，打印作业也会以 EMF 数据的形式显示在后台处理程序，从而允许在后台后台处理程序线程随后呈现 EMF 数据时快速返回到应用程序。

有关 EMF 数据类型的详细信息，请参阅 *windows 2000 专业资源工具包* 或 *Windows 2000 服务器资源工具包*。 有关增强型图元文件的详细信息，请参阅 Windows SDK 文档。  (这些资源可能在某些语言和国家/地区不可用。 ) 

 

 




