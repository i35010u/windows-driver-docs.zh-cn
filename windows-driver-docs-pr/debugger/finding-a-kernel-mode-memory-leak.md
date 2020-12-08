---
title: 查找内核模式内存泄漏
description: 查找内核模式内存泄漏
keywords:
- 内存泄漏，内核模式
- 内存泄漏，内核模式，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f703c034bb729849d6793fffb33f4e2015e4ef9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838197"
---
# <a name="finding-a-kernel-mode-memory-leak"></a>查找内核模式内存泄漏


使用以下技术来确定内核模式内存泄漏的原因：

[使用 PoolMon 查找内核模式内存泄漏](using-poolmon-to-find-a-kernel-mode-memory-leak.md)

[使用内核调试程序查找内核模式内存泄漏](using-the-kernel-debugger-to-find-a-kernel-mode-memory-leak.md)

[使用驱动程序验证程序查找内核模式内存泄漏](using-driver-verifier-to-find-a-kernel-mode-memory-leak.md)

如果不知道哪个内核模式驱动程序或组件负责泄露，则应首先使用 PoolMon 技术。 此方法显示与内存泄漏关联的池标记;使用此池标记的驱动程序或组件负责泄露。

如果已确定了负责的驱动程序或组件，请使用前面列表中的第二个和第三个方法来更明确地确定泄漏的原因。

 

 





