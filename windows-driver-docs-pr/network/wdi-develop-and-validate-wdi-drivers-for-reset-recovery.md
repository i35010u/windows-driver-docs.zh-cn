---
title: 开发和验证可重置恢复的 WDI 驱动程序
description: UE 有一个内置挂钩，用于通过模拟固件挂起来进行压力过大重置和恢复。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d8eb49b5166e923fb5432114dd0abd61b08ffa5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840593"
---
# <a name="develop-and-validate-wdi-drivers-for-reset-recovery"></a>开发和验证可重置恢复的 WDI 驱动程序


UE 有一个内置挂钩，用于通过模拟固件挂起来进行压力过大重置和恢复。 它会练习 UE 和 LE，而不是实际的固件，这在模拟中可能仍然有效。 代码位于 M1 UE 中。 如果 IHV 具有插入固件挂起的机制，则这是理想之选。 这将练习在 LE 下的模块上重置恢复，尤其是总线、ACPI 和 UEFI。 与重置恢复相关的这些较低层中存在很难调试的问题，其中较低层未能实际重置固件。

 

 





