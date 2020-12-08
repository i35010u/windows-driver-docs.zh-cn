---
title: 从网页安装打印驱动程序
description: 从网页安装打印驱动程序
keywords:
- Internet 打印 WDK，从网页安装驱动程序
- 打印网页 WDK，安装打印驱动程序
- 网页 WDK 打印机，从安装打印驱动程序
- 安装驱动程序 WDK 打印机、网页
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 121d49d0a67db4841f7b54410a036636128e7a19
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835681"
---
# <a name="installing-print-drivers-from-a-web-page"></a>从网页安装打印驱动程序





必须先从打印服务器发送驱动程序文件并将其安装在用户的系统上，然后用户才能将作业发送到打印队列。 当用户查看打印队列的网页，然后选择其安装页面时，将发生此安装操作。  (不能将安装页面替换为自定义页面。 ) 

如果客户端可以使用 RPC 连接到服务器（这可能是 intranet 连接），则将以通常的非 HTTP 方式安装打印机。 否则，安装页将调用 HTTP 打印服务器，该服务器会创建一个 cab 文件 (Microsoft Windows SDK 文档) 包含打印机的安装信息 (INF) 文件和所有必需的安装文件。 服务器会将 cabinet 文件发送到其扩展的客户端。 它启动客户端的 "添加打印机向导"，该向导完成安装并将打印机添加到用户的打印文件夹中。

除了选择打印队列的安装页，用户可以通过显式运行 "添加打印机向导" 来安装 URL 识别的打印机。 当用户指定 "添加打印机向导" 的 URL 时，客户端始终使用 HTTP 连接到服务器。

**注意**  安装包含自己的网卡并且因此未连接到服务器的打印机时，必须使用此安装方法。

 

除了指定 [打印机 inf 文件](printer-inf-files.md)的内容（用于在打印服务器上安装打印机的同一个 INF 文件）外，安装过程不能自定义。

 

 




