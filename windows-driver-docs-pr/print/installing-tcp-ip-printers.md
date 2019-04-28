---
title: 安装 TCP/IP 打印机
description: 安装 TCP/IP 打印机
ms.assetid: 15339cce-69aa-480d-bfee-11ea509ff5d4
keywords:
- TCP/IP WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b7bce0ae75003b7bc7648497afb8308a8871a0a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329603"
---
# <a name="installing-tcpip-printers"></a>安装 TCP/IP 打印机


使用 TCP/IP 的网络的打印机可以充分利用 TCP 端口监视器来安装和配置打印机的功能：

-   **自动发现**:在子网上的所有 TCP/IP 打印机自动发现和安装。

-   **自动选择**:TCP/IP 打印机安装时，根据从新打印机端口监视器管理信息基础 (MIB) 或 Tcpmon.ini 检索的信息，可自动选择的打印机驱动程序。

使用 Windows Vista 引入了这些功能。

### <a name="port-monitor-mibs"></a>端口监视器 Mib

打印机扩展的 MIB 规范提供了网络卡参数的更多的容量。 此扩展允许自定义仅在 Tcpmon.ini 在 Windows Vista 之前的 Windows 版本中存储的打印机信息。

通过使用此扩展的 MIB，可以管理的打印机信息的更新，而无需修改 Tcpmon.ini。 如果未实现扩展的 MIB，TCP 端口监视器将恢复为使用 Tcpmon.ini。

有关扩展的 MIB 规范的详细信息，请参阅[打印机端口监视器 MIB v1.0](https://go.microsoft.com/fwlink/p/?linkid=526286)打印机 Working Group 文档。

 

 




