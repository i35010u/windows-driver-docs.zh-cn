---
title: C28131
description: 警告 C28131 DriverEntry 例程应保存一份参数，而不是指针，因为 I/O 管理器释放缓冲区。
ms.assetid: 9661f17e-a19a-4230-a848-8233f635db09
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28131
ms.openlocfilehash: e6933b3a4c67a0ad71f2f4b372b4331944678e24
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361439"
---
# <a name="c28131"></a>C28131


警告 C28131:DriverEntry 例程应保存一份参数，而不是指针，因为 I/O 管理器释放缓冲区

在驱动程序*DriverEntry*例程指针的副本保存到缓冲区而不是保存缓冲区的副本。 因为释放缓冲区时*DriverEntry*例程返回时，指向缓冲区的指针很快就会无效。

 

 





