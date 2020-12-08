---
title: 将驱动程序移植到 64 位 Windows
description: 将驱动程序移植到 64 位 Windows
keywords:
- 64位 WDK 内核，将驱动程序移植到
- 将驱动程序移植到64位 Windows
- thunk WDK
- WOW64 thunk 层 WDK
- 将参数转换为固定精度类型
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a900f8e8dd3479b0e47be3dc566cbec0652c4410
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803815"
---
# <a name="porting-your-driver-to-64-bit-windows"></a>将驱动程序移植到 64 位 Windows





Windows 的64位版本旨在使开发人员能够对其32位和64位 Windows 应用程序使用单个源代码库。 在很大程度上，对于32位和64位 Windows 驱动程序也是如此。

对于用户模式的应用程序，64位 Windows 包含 windows on Windows (WOW64) *thunk 层* ，使32位应用程序能够执行 (，在64位版本的 Windows 上) 一些性能下降。 它通过以下方式实现此功能：在转换为64位内核之前，截获32位函数调用并将指针精度参数类型转换为固定精度类型。 此转换过程称为 *thunk*。

**注意**  仅对32位 *应用程序* 执行此 thunk;32位版本的 Windows 64 上不支持位 *驱动程序* 。

 

 

 




