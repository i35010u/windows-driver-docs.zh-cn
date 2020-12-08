---
title: 打印驱动程序包
description: 打印驱动程序包
keywords:
- 安装驱动程序 WDK 打印机、包
- 打印机驱动程序安装 WDK，包
- 包 WDK 打印
- 驱动程序包 WDK 打印
- 打印机驱动程序包 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a7cdc2fe2760bc944924df17b33f132500c415f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807485"
---
# <a name="print-driver-packages"></a>打印驱动程序包


在 Windows Vista 中，安装和打印基础结构尽可能使用完整的驱动程序包。 驱动程序包由您必须提供的所有硬件和软件组件组成，以便您的设备在 Windows 下受支持。

用于打印机安装的驱动程序包选项包括以下各项：

-   **本地打印机安装。** 当用户在 Windows Vista 计算机上安装新的打印机驱动程序时，安装程序会自动将完整的打印驱动程序包添加到驱动程序存储区，然后安装该驱动程序。

-   **远程打印机安装。** 当用户在远程 Windows Vista 计算机上安装打印驱动程序时，安装程序会将打印驱动程序包添加到远程计算机上的驱动程序存储区，然后从远程计算机上的驱动程序存储区中安装打印驱动程序。

-   **包点和打印。** 当 Windows Vista 客户端连接到另一台运行 Windows Vista 的计算机上的共享打印机，并且它需要下载驱动程序时，包点和打印将驱动程序包从远程打印服务器上的驱动程序存储区复制到客户端上的驱动程序存储区。 然后，"包点" 和 "打印" 将从本地驱动程序存储区将驱动程序安装在本地计算机上。

-   **Web 包点和打印。** 如果 Windows Vista 客户端使用超文本传输协议 (HTTP) 连接到 Windows Vista 打印服务器托管的共享打印机，并且具有驱动程序包，则 web 包点和打印将以与包点和打印相同的方式安装驱动程序。

本节包括：

[点选打印与驱动程序包](point-and-print-with-driver-packages.md)

[包感知打印驱动程序](package-aware-print-drivers.md)

[使用更新的核心打印驱动程序](using-updated-core-print-drivers.md)

 

 




