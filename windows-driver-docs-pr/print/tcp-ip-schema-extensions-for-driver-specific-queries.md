---
title: 驱动程序特定查询的 TCP/IP 架构扩展
description: 驱动程序特定查询的 TCP/IP 架构扩展
ms.assetid: c6f85f99-852a-418f-98da-41fe4c36e9ba
keywords:
- TCP/IP 架构扩展 WDK 打印机
- 架构扩展 WDK TCP/IP
- 特定于驱动程序查询 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3cd7fd6c4eaab33582de07c24b065c5e7b2a44f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568295"
---
# <a name="tcpip-schema-extensions-for-driver-specific-queries"></a>驱动程序特定查询的 TCP/IP 架构扩展


按前面所述，标准 TCP/IP 端口监视器支持标准的打印架构的子集，以便每个驱动程序可以发送查询并了解响应。 但是，特定的驱动程序可能需要存储在打印机的 MIB 中的其他信息。

对于查询有关典型打印机属性，必须创建包含定义的属性的查询。 以下主题介绍三种构造 Tcpbidi.xsd 文件中定义的并提供一种方法来检索此类信息。

[Const](const.md)

[Converter](converter.md)

[安装](installed2.md)

[值](value.md)

 

 




