---
title: 打印驱动程序包
description: 打印驱动程序包
ms.assetid: 902e1634-e705-4902-baab-a93818288b08
keywords:
- 安装驱动程序 WDK 打印机，包
- 打印机驱动程序安装 WDK，包
- 包 WDK 打印
- 驱动程序包 WDK 打印
- 打印机驱动程序包 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bea539224ece6f6c75b36b799e5478879a8b10c9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389476"
---
# <a name="print-driver-packages"></a>打印驱动程序包


在 Windows Vista 中，安装程序和打印基础结构使用尽可能完整的驱动程序包。 必须提供使你的设备以支持在 Windows 下的所有硬件和软件组件的包含驱动程序包。

安装打印机驱动程序的包选项包括：

-   **本地打印机安装。** 当用户在 Windows Vista 计算机上安装新的打印机驱动程序时，安装程序自动将完成的打印驱动程序包添加到驱动程序存储区，，然后安装该驱动程序。

-   **远程打印机安装。** 当用户在远程 Windows Vista 计算机上安装打印驱动程序时，安装程序将打印驱动程序程序包添加到远程计算机上的驱动程序存储，，然后从驱动程序存储在远程计算机上安装打印驱动程序。

-   **包指向并打印。** 当 Windows Vista 客户端连接到运行的 Windows Vista 的另一台计算机上的共享打印机，并且它需要下载该驱动程序时，包的点和打印副本驱动程序包从驱动程序存储区将远程打印服务器上的驱动程序存储上客户端。 然后打包点，并打印从本地驱动程序存储在本地计算机上安装驱动程序。

-   **Web 包点和打印。** 当 Windows Vista 客户端使用超文本传输协议 (HTTP) 连接到托管的 Windows Vista 打印服务器和包含驱动程序包、 web 包点的共享打印机和打印安装驱动程序作为包指向并打印相同的方式。

本部分包括：

[指向并打印与驱动程序包](point-and-print-with-driver-packages.md)

[识别包的打印驱动程序](package-aware-print-drivers.md)

[使用更新的核心打印驱动程序](using-updated-core-print-drivers.md)

 

 




