---
title: 回调对象
description: 回调对象
keywords:
- 同步 WDK 内核，回调对象
- 回叫对象 WDK 内核
- 对象 WDK 回叫对象
- 内核回调机制 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 669c07f7b823132acf6ca13d929cb9996c951aa6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838781"
---
# <a name="callback-objects"></a>回调对象





内核的回调机制为驱动程序提供了一种常规方法，在满足某些条件时提供通知。

驱动程序可以创建回调对象，其他驱动程序可以请求与此驱动程序定义的回调相关联的条件的通知。 此外，系统还为驱动程序使用定义了两个回调对象。

每个回调对象都有一个名称和一组属性，在创建对象时定义。 系统定义的回调对象命名为 **\\ callback \\ SetSystemTime**、 **\\ 回叫 \\ PowerState** 和 **\\ 回调 \\ ProcessorAdd**; 驱动程序定义的回调不得重复这些名称。

若要从系统或驱动程序定义的回调请求通知，驱动程序会打开回调对象并注册回调例程。 为回调定义的条件变为 true 时，其创建者会触发通知。 进而，系统会调用为回调注册的所有回调例程。

本节包含下列主题：

[定义回调对象](defining-a-callback-object.md)

[使用驱动程序定义的回调对象](using-a-driver-defined-callback-object.md)

[使用系统定义的回调对象](using-a-system-defined-callback-object.md)

 

 




