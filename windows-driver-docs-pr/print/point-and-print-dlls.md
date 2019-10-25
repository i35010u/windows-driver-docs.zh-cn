---
title: 点选打印 DLL
description: 点选打印 DLL
ms.assetid: 7ead940e-8426-4756-890f-f3607dc1f9ca
keywords:
- 指向和打印 WDK，Dll
- Dll WDK 点和打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f90fa9f1653422bd0f445a13f5af6222402148a8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842355"
---
# <a name="point-and-print-dlls"></a>点选打印 DLL





您可以选择提供特殊的点和打印 DLL，方法是将其名称与**Module**注册表值相关联。 此 DLL 必须导出以下两个函数：

<a href="" id="generatecopyfilepaths"></a>[**GenerateCopyFilePaths**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-generatecopyfilepaths)  
此函数由服务器的后台处理程序和客户端的后台处理程序调用，可用于修改**目录**注册表值指定的目录路径。 可以修改源路径（服务器上）或目标路径（在客户端上）或同时修改两者。

<a href="" id="spoolercopyfileevent"></a>[**SpoolerCopyFileEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent)  
此函数也被服务器的后台处理程序和客户端的后台处理程序调用，接收到一个指示与连接相关的特定打印机事件发生的事件代码。

点和打印 DLL 不需要仅导出这些函数。 例如，Microsoft 的 ICM 组件使用的 Mscms .dll 还会导出一组 ICM API 函数。

请注意，你可以指定其他 Dll，还可以指定导出**GenerateCopyFilePaths**和**SpoolerCopyFileEvent**的点和打印 dll。 为此，请将 DLL 文件名指定给**Files**注册表项，而不是**Module**注册表项。 （请参阅[安装队列特定的文件](installing-queue-specific-files.md)）。

在安装应用程序通过调用**SetPrinterDataEx**将 dll 的名称放入服务器的注册表中后，所有对**SetPrinterDataEx**的后续调用将导致调用 DLL 的[**SpoolerCopyFileEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent)函数，并使用已提供 COPYFILE\_事件的事件代码\_将\_打印机\_DATAEX。

与 "**文件**" 注册表项中列出的文件不同（请参阅[安装队列特定的文件](installing-queue-specific-files.md)），当客户端连接到打印机时，不会将点和打印 DLL 从打印服务器复制到客户端。 相反，在建立与打印服务器的连接时，将假定该 DLL 已是客户端驻留的。 因此，DLL 可用于与点和打印功能无关的其他目的。

在客户端上安装点和打印 DLL 的一种方法是在[打印机 INF 文件](printer-inf-files.md)中指定其名称作为依赖文件，以便在[下载驱动程序特定文件](downloading-driver-specific-files.md)的过程中，可以将该文件复制到客户端的驱动程序目录。

 

 




