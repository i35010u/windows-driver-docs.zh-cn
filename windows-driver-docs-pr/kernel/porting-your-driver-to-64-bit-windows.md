---
title: 移植到 64 位 Windows 驱动程序
description: 移植到 64 位 Windows 驱动程序
ms.assetid: f06e6aae-fc44-481c-a277-1c266d6e6d7b
keywords:
- 64 位 WDK 内核，移植到驱动程序
- 移植到 64 位 Windows 的驱动程序
- 形式转换 WDK
- WOW64 形式转换层 WDK
- 将参数转换为固定精度的类型
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cda3cbfe6771a49e8ae899a54cd85918920bd963
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525795"
---
# <a name="porting-your-driver-to-64-bit-windows"></a>移植到 64 位 Windows 驱动程序





Windows 的 64 位版本旨在使开发人员可以使用单个源代码库为 32 位和 64 位 Windows 应用程序。 很大程度，这也是 32 位和 64 位 Windows 驱动程序，则返回 true。

64 位 Windows 的用户模式应用程序，包括 Windows (WOW64) 上的 Windows*形式转换层*，它使 64 位版本的 Windows 32 位应用程序 （使用一些性能下降） 来执行。 之所以如此是因为截获 32 位函数调用和在 64 位内核转换之前将指针精度参数类型转换为相应的固定精度类型。 此转换过程称为*形式转换*。

**请注意**  此形式转换只能是针对 32 位*应用程序*; 32 位*驱动程序*不支持在 64 位版本的 Windows 上。

 

 

 




