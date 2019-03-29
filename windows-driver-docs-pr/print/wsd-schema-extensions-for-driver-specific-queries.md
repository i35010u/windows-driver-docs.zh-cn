---
title: 驱动程序特定查询的 WSD 架构扩展
description: 驱动程序特定查询的 WSD 架构扩展
ms.assetid: 508a9f87-8fd2-4c95-8efb-5d1d7201981a
keywords:
- WSD 架构扩展 WDK 打印机
- 架构扩展 WDK WSD
- 特定于驱动程序查询 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f3eb2b76e34da8f3b025e4905692c1c0cde5992
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566026"
---
# <a name="wsd-schema-extensions-for-driver-specific-queries"></a>驱动程序特定查询的 WSD 架构扩展


如中所述[自定义打印机端口监视器](customizing-the-printer-port-monitors.md)，Web Services for Devices (WSD) 端口监视器支持标准的子集打印架构，以便每个驱动程序可以发送查询并了解响应。 但是，特定的驱动程序可能需要通过打印机的 Web 服务接口的其他信息。

对于查询有关典型打印机属性，必须创建包含定义的属性的查询。 下面的主题介绍了四个 WsdBidi.xsd 文件中定义的提供一种方法来检索此类信息构造。

[Const](const.md)

[安装](installed.md)

[列表](list.md)

[值](value.md)

 

 




