---
title: 开发和验证可重置恢复的 WDI 驱动程序
description: UE 具有内置挂钩的压力重置和恢复通过模拟固件挂起过大。
ms.assetid: 5C669F22-2C82-4072-8010-1DDC918C064F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed2fc1b25c031378fefa96be457ffb159e7f5c37
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330508"
---
# <a name="develop-and-validate-wdi-drivers-for-reset-recovery"></a>开发和验证可重置恢复的 WDI 驱动程序


UE 具有内置挂钩的压力重置和恢复通过模拟固件挂起过大。 它执行 UE 和 LE 但不是实际固件，这可能仍然可以模拟中正常工作。 代码位于 M1 UE。 如果 IHV 具有机制注入固件挂起，则是理想之选。 此练习中对模块下面 LE、 重置恢复专门总线、 ACPI 和 UEFI。 这些较低层中已硬调试问题有关的较低层无法实际重置固件重置恢复。

 

 





