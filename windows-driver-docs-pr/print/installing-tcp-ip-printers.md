---
title: 安装 TCP/IP 打印机
description: 安装 TCP/IP 打印机
ms.assetid: 15339cce-69aa-480d-bfee-11ea509ff5d4
keywords:
- TCP/IP WDK 打印机
ms.date: 06/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4840bcb4459c6c7bb7d5ad3e2e3ee36e62cb74b8
ms.sourcegitcommit: a16fd2876383265b4ad336dea624e4b13fc13a1b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88644015"
---
# <a name="installing-tcpip-printers"></a>安装 TCP/IP 打印机

使用 TCP/IP 的网络打印机可以利用 TCP 端口监视器的功能来安装和配置打印机：

- **自动发现**：会自动找到并安装子网上的所有 tcp/ip 打印机。

- **自动选择**：根据从新的打印机端口监视器管理信息基础 (MIB) 或 Tcpmon.ini 检索的信息，在安装 tcp/ip 打印机时，可以自动选择打印机驱动程序。

Windows Vista 引入了这些功能。

## <a name="port-monitor-mibs"></a>端口监视器 Mib

适用于打印机的扩展 MIB 规范为网卡参数提供额外的容量。 此扩展允许自定义仅存储在 Windows Vista 之前的 Windows 版本中的 Tcpmon.ini 的打印机信息。

通过使用此扩展的 MIB，你可以管理打印机信息的更新，而无需修改 Tcpmon.ini。 如果未实现扩展 MIB，则 TCP 端口监视器将恢复为使用 Tcpmon.ini。

有关扩展 MIB 规范的详细信息，请参阅 [打印机端口监视器 MIB v1.0 (PDF 下载) ](https://go.microsoft.com/fwlink/p/?linkid=526286) 打印机工作组文档。
