---
title: 驱动程序特定查询的 TCP/IP 架构扩展
description: 驱动程序特定查询的 TCP/IP 架构扩展
keywords:
- TCP/IP 架构扩展 WDK 打印机
- 架构扩展 WDK TCP/IP
- 特定于驱动程序的查询 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5968d7833633290f11599e2e629ab7a9902c304
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806749"
---
# <a name="tcpip-schema-extensions-for-driver-specific-queries"></a>驱动程序特定查询的 TCP/IP 架构扩展


如前所述，标准 TCP/IP 端口监视器支持标准打印架构的一部分，因此每个驱动程序都可以发送查询并了解响应。 但是，特定的驱动程序可能需要存储在打印机 MIB 中的其他信息。

对于涉及典型打印机属性的查询，您必须创建包含您定义的属性的查询。 以下主题介绍 Tcpbidi 文件中定义的三个构造，并提供一种方法来检索此类信息。

[Const](const.md)

[Converter](converter.md)

[已安装](installed2.md)

值

 

 




