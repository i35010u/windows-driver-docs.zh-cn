---
title: 驱动程序特定查询的 WSD 架构扩展
description: 驱动程序特定查询的 WSD 架构扩展
keywords:
- WSD 架构扩展 WDK 打印机
- 架构扩展 WDK WSD
- 特定于驱动程序的查询 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4c99a6131feae5bcdb09e0b327ef439787694d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785775"
---
# <a name="wsd-schema-extensions-for-driver-specific-queries"></a>驱动程序特定查询的 WSD 架构扩展


如 [自定义打印机端口监视器](customizing-the-printer-port-monitors.md)中所述，适用于设备的 Web 服务 (WSD) 端口监视器支持标准打印架构的一部分，因此每个驱动程序都可以发送查询并了解响应。 但是，特定的驱动程序可能需要其他信息，这些信息可通过打印机的 Web 服务界面获得。

对于涉及典型打印机属性的查询，您必须创建包含您定义的属性的查询。 以下主题介绍了 WsdBidi 文件中定义的四个构造，提供一种方法来检索此类信息。

[Const](const.md)

[已安装](installed.md)

[列表](list.md)

值

 

 




