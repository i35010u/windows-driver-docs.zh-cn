---
title: 安装 TCP/IP 打印机
description: 安装 TCP/IP 打印机
ms.assetid: 15339cce-69aa-480d-bfee-11ea509ff5d4
keywords:
- TCP/IP WDK 打印机
ms.date: 06/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: b990999a2a9ab0c47a3926cad06c45e5fdf26425
ms.sourcegitcommit: 581fb777a2376854ca12e767d366e2cb79724b73
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2020
ms.locfileid: "84461832"
---
# <a name="installing-tcpip-printers"></a>安装 TCP/IP 打印机

使用 TCP/IP 的网络打印机可以利用 TCP 端口监视器的功能来安装和配置打印机：

- **自动发现**：会自动找到并安装子网上的所有 tcp/ip 打印机。

- **自动选择**：根据从新的打印机端口监视器管理信息库（MIB）或 Tcpmon 中检索到的信息安装 tcp/ip 打印机时，可以自动选择打印机驱动程序。

Windows Vista 引入了这些功能。

## <a name="port-monitor-mibs"></a>端口监视器 Mib

适用于打印机的扩展 MIB 规范为网卡参数提供额外的容量。 此扩展允许自定义仅存储在 windows Vista 之前的 Windows 版本中的 Tcpmon 的打印机信息。

通过使用此扩展的 MIB，你可以管理打印机信息的更新，而无需修改 Tcpmon。 如果未实现扩展 MIB，则 TCP 端口监视器将恢复为使用 Tcpmon。

有关扩展 MIB 规范的详细信息，请参阅[打印机端口监视器 MIB 1.0](https://go.microsoft.com/fwlink/p/?linkid=526286)版打印机工作组文档。
