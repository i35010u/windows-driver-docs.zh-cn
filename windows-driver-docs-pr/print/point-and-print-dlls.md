---
title: 点选打印 DLL
description: 点选打印 DLL
ms.assetid: 7ead940e-8426-4756-890f-f3607dc1f9ca
keywords:
- 指向并打印 WDK Dll
- Dll WDK 指向并打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b5e9da73dc21c9620b37b4247a38821d4b2879c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383535"
---
# <a name="point-and-print-dlls"></a>点选打印 DLL





您可以选择可提供通过将其与名称相关联的特殊点和打印 DLL**模块**注册表值。 此 DLL 必须导出以下两个函数：

<a href="" id="generatecopyfilepaths"></a>[**GenerateCopyFilePaths**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-generatecopyfilepaths)  
可以使用此函数，它由服务器的后台处理程序和客户端的后台处理程序调用，来修改指定的目录路径**Directory**注册表值。 （在服务器上） 的源路径或目标路径 （位于客户端），或两者，可以进行修改。

<a href="" id="spoolercopyfileevent"></a>[**SpoolerCopyFileEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-spoolercopyfileevent)  
此函数，也称为服务器的后台处理程序和客户端的后台处理程序，接收，该值指示某些与连接相关打印机事件的匹配项的事件代码。

点和打印 DLL 不需要导出只能使用这些功能。 例如 Mscms.dll，由 Microsoft 的 ICM 组件也会导出一组 ICM API 函数。

请注意，您可以指定其他 Dll 此外或而不是、 点和打印将导出的 DLL **GenerateCopyFilePaths**并**SpoolerCopyFileEvent**。 若要执行此操作，将分配到的 DLL 文件名称**文件**注册表项，而不是**模块**注册表项。 (请参阅[安装特定于队列的文件](installing-queue-specific-files.md))。

在安装后应用程序在放入了 DLL 的名称服务器的注册表通过调用**SetPrinterDataEx**，则所有后续调用**SetPrinterDataEx**导致调用 DLL 的[ **SpoolerCopyFileEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-spoolercopyfileevent)函数，其提供的事件代码为 COPYFILE\_事件\_设置\_打印机\_DATAEX。

与下列出的文件不同**文件**注册表项 (请参阅[安装特定于队列的文件](installing-queue-specific-files.md))，点和打印 DLL 不会复制从打印服务器到客户端时客户端连接到打印机. 相反，则假定 DLL 已为客户端驻留在与打印服务器的连接时进行。 因此，可以为指向和打印功能与不相关的其他目的使用 DLL。

在客户端上安装点和打印 DLL 的一种方法是指定其名称中的[打印机 INF 文件](printer-inf-files.md)为依赖文件，因此可以将文件复制到客户端的驱动程序目录期间[的下载特定于驱动程序文件](downloading-driver-specific-files.md)。

 

 




