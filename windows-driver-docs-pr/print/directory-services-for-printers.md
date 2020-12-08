---
title: 打印机的目录服务
description: 打印机的目录服务
keywords:
- 目录服务 WDK 打印机
- 打印机目录服务支持 WDK
- 打印队列 WDK，目录服务
- 队列 WDK 打印机，目录服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cd1ec1c3f5c0ae866bc3d68a69ab29e7247c382
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797207"
---
# <a name="directory-services-for-printers"></a>打印机的目录服务





当用户安装网络共享打印机时，默认情况下，Windows 2000 和更高版本的打印文件夹还会将打印机发布到 Windows 2000 (或更高版本) 目录服务。 可以通过使用打印机信息的输入结构 **SetPrinter** \_ \_ （如 Microsoft Windows SDK 文档中所述）调用后台处理程序的 SetPrinter 函数来完成发布。

发布打印队列后，用户可以通过任务栏的 "**开始**" 菜单上的 "**搜索**" 选项查看该队列。

以下主题提供了有关目录服务的打印机支持的详细信息：

[打印机目录服务的打印后台处理程序支持](print-spooler-support-for-printer-directory-services.md)

[打印机目录服务的打印机驱动程序支持](printer-driver-support-for-printer-directory-services.md)

 

 




