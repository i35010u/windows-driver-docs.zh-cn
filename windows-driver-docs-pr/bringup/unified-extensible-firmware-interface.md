---
title: 统一可扩展固件接口 (UEFI)
description: 统一可扩展固件接口 (UEFI)
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5736e2f9b0e135a62483059be3c9cbab5aded93c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525614"
---
# <a name="unified-extensible-firmware-interface-uefi"></a>统一可扩展固件接口 (UEFI) 


截至 Windows 10，版本 1703年 （在编写本文档时的时间），Microsoft 需要 UEFI 规范版本 2.3.1c。 由于 UEFI.org 一直更新规范文档和改进具有这些更新的源，最终将更改此要求。

在 Microsoft 内部，我们认为 UEFI 规范 2.5 和 2.6 中出现一些措辞歧义。 因此我们尚未更新到这些规范版本。 但是的规范版本不会影响 UEFI 源代码树。 

在实现 UEFI 代码时，请确保使用与主分支的最新位，并使用最新的 UEFI 规范文档中的指南构建生成源分支。

没有适用于各种安全功能的 UEFI 规范文档中更新的功能。 例如 UEFI 规范 2.6"4.6 EFI 配置表属性 （& t）"部分中的第 107 页专门中添加对"EFI_MEMORY_ATTRIBUTES_TABLE"的支持。

-   内存属性表 (MAT):

    -   EFI\_内存\_属性\_表。 整个 UEFI 运行时必须由此表进行描述。

    -   所有条目必须都包含属性 EFI\_内存\_RO、 EFI\_内存\_XP 中，或两者。 内存只允许处于以下两种状态：可读取且可执行，或者可写入且不可执行。

Windows 10，版本 1703，截至到 UEFI 规范与安全启动模式有关最新的更新不完全支持通过 Windows。 正在为未来的 Windows 调查新的安全启动模式的支持版本。

## <a name="related-resources"></a>相关资源

[UEFI 规范文档](https://www.uefi.org/specifications)





