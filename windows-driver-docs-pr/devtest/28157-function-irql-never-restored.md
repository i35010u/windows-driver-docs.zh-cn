---
title: C28157
description: 警告 C28157 不会还原 IRQL。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28157
ms.openlocfilehash: ed690171704f32536566ea5f4d2b519bef0cf35a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793157"
---
# <a name="c28157"></a>C28157


警告 C28157：不还原 IRQL

当前函数的 **\_ \_ 还原 \_** 批注需要使用 irql，后者要求完成时，驱动程序应在从以前的 irql 值还原的 irql 下执行。 但是，在该函数完成时，至少有一个路径在不同的 IRQL 处执行驱动程序。

 

 





