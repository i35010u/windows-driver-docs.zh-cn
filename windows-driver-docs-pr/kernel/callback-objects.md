---
title: 回调对象
description: 回调对象
ms.assetid: d6ccb064-5936-4996-a5cd-795803958b5d
keywords:
- 同步 WDK 内核，回调对象
- 回调对象 WDK 内核
- 对象 WDK 回调对象
- 内核回调机制 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb0b163efdc27101f7dbeb7df7fd3c8a2f2169c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524286"
---
# <a name="callback-objects"></a>回调对象





内核的回调机制，提供要请求并满足某些条件时提供通知的驱动程序的常规方法。

驱动程序可以创建一个回调对象和其他驱动程序可以请求与此驱动程序定义的回调关联的条件的通知。 此外，系统定义驱动程序使用的两个回调的对象。

每个回调对象具有名称和一组属性，该对象创建时定义。 系统定义的回调对象的命名**\\回调\\SetSystemTime**， **\\回调\\PowerState**，和**\\回调\\ProcessorAdd**; 驱动程序定义的回调必须重复这些名称。

若要从系统或驱动程序定义的回调请求通知，驱动程序打开回调对象，并注册回调例程。 当回调所定义的条件变为 true 时，其创建者就会触发通知。 反过来，系统调用的回调注册的所有回调例程。

本部分包含以下主题：

[定义回调对象](defining-a-callback-object.md)

[使用驱动程序定义的回调对象](using-a-driver-defined-callback-object.md)

[使用系统定义的回调对象](using-a-system-defined-callback-object.md)

 

 




