---
title: C28131
description: 警告 C28131 DriverEntry 例程应保存参数的副本，而不是指针，因为 i/o 管理器会释放缓冲区。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28131
ms.openlocfilehash: 41bafd1b12b4256598adaa1823847692a3781cb7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840411"
---
# <a name="c28131"></a>C28131


警告 C28131： DriverEntry 例程应保存参数的副本，而不是指针，因为 i/o 管理器释放缓冲区

驱动程序的 *DriverEntry* 例程会将指针副本保存到缓冲区，而不是保存缓冲区的副本。 由于缓冲区在 *DriverEntry* 例程返回时释放，因此指向缓冲区的指针很快就会无效。

 

 





