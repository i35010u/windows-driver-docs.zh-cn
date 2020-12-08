---
title: 点选打印 DLL
description: 点选打印 DLL
keywords:
- 指向和打印 WDK，Dll
- Dll WDK 点和打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fb705a5949d2f75ab64d1a828213f11182de07a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807565"
---
# <a name="point-and-print-dlls"></a>点选打印 DLL





您可以选择提供特殊的点和打印 DLL，方法是将其名称与 **Module** 注册表值相关联。 此 DLL 必须导出以下两个函数：

<a href="" id="generatecopyfilepaths"></a>[**GenerateCopyFilePaths**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-generatecopyfilepaths)  
此函数由服务器的后台处理程序和客户端的后台处理程序调用，可用于修改 **目录** 注册表值指定的目录路径。 服务器上的源路径 () 或客户) 端上 (的目标路径，或者两者都可以修改。

<a href="" id="spoolercopyfileevent"></a>[**SpoolerCopyFileEvent**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent)  
此函数也被服务器的后台处理程序和客户端的后台处理程序调用，接收到一个指示与连接相关的特定打印机事件发生的事件代码。

点和打印 DLL 不需要仅导出这些函数。 例如 Mscms.dll （由 Microsoft 的 ICM 组件使用）还会导出一组 ICM API 函数。

请注意，你可以指定其他 Dll，还可以指定导出 **GenerateCopyFilePaths** 和 **SpoolerCopyFileEvent** 的点和打印 dll。 为此，请将 DLL 文件名指定给 **Files** 注册表项，而不是 **Module** 注册表项。  (参阅) [安装 Queue-Specific 文件](installing-queue-specific-files.md) 。

在安装应用程序通过调用 **SetPrinterDataEx** 将 dll 的名称放入服务器的注册表中后，所有对 **SetPrinterDataEx** 的后续调用将导致调用 DLL 的 [**SpoolerCopyFileEvent**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent) 函数，并提供事件代码 COPYFILE \_ 事件 \_ 集 \_ PRINTER \_ DATAEX。

与 " **文件** " 注册表项中列出的文件不同 (参阅) [安装 Queue-Specific 文件](installing-queue-specific-files.md) ，当客户端连接到打印机时，不会将点和打印 DLL 从打印服务器复制到客户端。 相反，在建立与打印服务器的连接时，将假定该 DLL 已是客户端驻留的。 因此，DLL 可用于与点和打印功能无关的其他目的。

在客户端上安装点和打印 DLL 的一种方法是在 [打印机 INF 文件](printer-inf-files.md) 中指定其名称作为依赖文件，以便在 [下载驱动程序特定文件](downloading-driver-specific-files.md)的过程中，可以将该文件复制到客户端的驱动程序目录。

 

