---
title: 指向并打印简介
description: 指向并打印简介
ms.assetid: 03902c64-29d7-4b59-a604-e282e4a2c7ae
keywords:
- 指向并打印 WDK，有关指向并打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5dbaa132da1483597b243d48302339732ac2c5fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541393"
---
# <a name="introduction-to-point-and-print"></a>指向并打印简介





*指向并打印*是一个术语，指的是允许用户在 Windows 2000 和更高版本的客户端上的功能而无需提供磁盘或其他安装媒体创建到远程打印机的连接。 所有必要的文件和配置信息是自动从打印服务器下载到客户端。

指向并打印技术提供了两种方法可以依据指定应在客户端计算机从打印服务器发送的文件：

-   文件可以与打印机驱动程序相关联。 这些文件是与使用的驱动程序的每个打印队列关联。

-   文件可以与单个打印队列相关联。

有关详细信息，请参阅[支持点和打印机安装期间打印](supporting-point-and-print-during-printer-installations.md)。

当用户应用程序调用**AddPrinterConnection**函数 （Microsoft Windows SDK 文档中所述） 若要使打印机连接，执行以下操作：

-   驱动程序关联和队列相关联的文件从打印服务器下载到客户端。

-   当前值的打印机的配置参数，存储在打印机的项下的服务器的注册表中，会下载到客户端。

有关详细信息，请参阅[支持点和打印期间打印机连接](supporting-point-and-print-during-printer-connections.md)。

 

 




