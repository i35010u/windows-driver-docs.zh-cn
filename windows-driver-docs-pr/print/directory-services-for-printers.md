---
title: 打印机的目录服务
description: 打印机的目录服务
ms.assetid: 4b368602-67d9-4d26-a82b-8d14d8da2625
keywords:
- 目录服务 WDK 打印机
- 打印机目录服务支持 WDK
- 打印队列 WDK、 Directory 服务
- 队列 WDK 打印机，目录服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e070c46922ff8a545f7c5f87d5507ba0d781384f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371029"
---
# <a name="directory-services-for-printers"></a>打印机的目录服务





当用户安装的网络共享打印机，Windows 2000 和更高版本打印文件夹中，默认情况下，还会发布到 Windows 2000 （或更高版本） 的打印机目录服务。 发布通过调用的后台处理程序来实现**SetPrinter**函数中的打印机的输入结构\_信息\_7，Microsoft Windows SDK 文档中所述。

发布打印队列会使用户可通过对可见**搜索**任务栏上的选项**启动**菜单。

以下主题提供有关对目录服务的打印机支持的详细信息：

[打印后台处理程序支持的打印机目录服务](print-spooler-support-for-printer-directory-services.md)

[打印机目录服务的打印机驱动程序支持](printer-driver-support-for-printer-directory-services.md)

 

 




