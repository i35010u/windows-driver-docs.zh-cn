---
title: 从网页安装打印驱动程序
description: 从网页安装打印驱动程序
ms.assetid: 44da45f7-687c-4c54-9ee6-79c91fce3947
keywords:
- Internet 打印 WDK，并从 Web pages 安装驱动程序
- 打印网页 WDK，安装的打印驱动程序
- 网页 WDK 打印机，安装的打印驱动程序
- 安装驱动程序 WDK 打印机，网页
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69b7bfff32d8fd4f564599d4560a22b5e52068c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329617"
---
# <a name="installing-print-drivers-from-a-web-page"></a>从网页安装打印驱动程序





用户可以将作业发送到通过打印的网页可见的打印队列之前，必须从打印服务器发送和用户的系统上安装驱动程序文件。 当用户查看打印队列的 Web 页，然后选择其安装页时，会发生此安装操作。 （安装页不能替换为自定义页面。）

如果客户端可以连接到使用 RPC，很可能用于 intranet 连接，在服务器中常用的、 非 HTTP 方式安装打印机。 否则安装页会调用 HTTP 打印服务器，这将创建 （Microsoft Windows SDK 文档中所述） 的 cab 文件包含打印机的安装程序信息 (INF) 文件和所有必需的安装文件。 服务器将 cab 文件发送到客户端，它处于展开状态。 启动客户端的添加打印机向导，该向导完成安装，并将打印机添加到用户的打印文件夹。

作为选择打印队列的安装页面上的替代方法，用户可以通过显式运行添加打印机向导安装 URL 标识的打印机。 当用户指定的 URL 添加打印机向导时，客户端始终连接到使用 HTTP 服务器。

**请注意**  安装打印机，包含其自己的网卡，因此不连接到服务器时，必须使用此安装方法。

 

安装过程不超出指定的内容可自定义[打印机 INF 文件](printer-inf-files.md)，这是用于在打印服务器上安装打印机的同一个 INF 文件。

 

 




