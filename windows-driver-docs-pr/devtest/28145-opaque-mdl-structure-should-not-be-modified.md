---
title: C28145
description: 警告 C28145 不透明 MDL 结构不应由驱动程序修改。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28145
ms.openlocfilehash: 0cb7dd4feadb9b4f2740a533af715b4b9f4cb478
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793193"
---
# <a name="c28145"></a>C28145


警告 C28145：不透明 MDL 结构不应由驱动程序修改

驱动程序代码正在更改 MDL 结构的成员。

**MdlFlags** 字段用作所有 MDL 字段的代理。 不应修改任何字段，但 MDL \_ 映射 \_ 可能会 \_ 失败，后者用于需要 Microsoft Windows 98 或 WINDOWS NT (SP4) 兼容的驱动程序和 \_ 已锁定的 MDL 页面（用于 \_ 需要与 Windows 2000 兼容的驱动程序的驱动程序）。

 

 





