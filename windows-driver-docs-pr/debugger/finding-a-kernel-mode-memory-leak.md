---
title: 查找内核模式内存泄漏
description: 查找内核模式内存泄漏
ms.assetid: 7e707b89-8614-46d7-9c2e-bea2ddf16164
keywords:
- 内存泄漏、 内核模式
- 内存泄漏、 内核模式下概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5de6d820114d0f3af2b0b791b40cf0c0d135b28d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564393"
---
# <a name="finding-a-kernel-mode-memory-leak"></a>查找内核模式内存泄漏


使用以下方法来确定内核模式内存泄露的原因：

[使用 PoolMon 查找内核模式内存泄漏](using-poolmon-to-find-a-kernel-mode-memory-leak.md)

[使用内核调试程序来查找内核模式内存泄漏](using-the-kernel-debugger-to-find-a-kernel-mode-memory-leak.md)

[使用驱动程序验证程序来查找内核模式内存泄漏](using-driver-verifier-to-find-a-kernel-mode-memory-leak.md)

如果不知道哪个内核模式驱动程序或组件负责泄漏，你应首先使用 PoolMon 方法。 此方法会显示与内存泄漏; 关联的池标记驱动程序或组件，它使用此池标记负责泄漏。

如果已经确定负责驱动程序或组件，使用上面的列表中的第二个和第三个技术来更具体地说确定泄露的原因。

 

 





