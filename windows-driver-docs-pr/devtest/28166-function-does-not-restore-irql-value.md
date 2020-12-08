---
title: C28166
description: 警告 C28166 该函数不会将 IRQL 恢复为当前位于函数入口的值，并且此操作是必需的。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28166
ms.openlocfilehash: 5d97c5947d98a32b72eb0aa0a5c3399fe69c8b71
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793129"
---
# <a name="c28166"></a>C28166


警告 C28166：该函数不会将 IRQL 恢复为当前位于函数入口的值，并且此操作是必需的。

此警告意味着函数的 **\_ irql \_ 要求使用 \_ 相同 \_** 的批注，并且至少有一个通过函数的路径，但函数退出会将 IRQL 还原到在函数项上运行驱动程序的 irql。

通常， **\_ IRQL \_ 要求 \_ \_** 在回调函数上使用相同的批注。

若要避免此警告，驱动程序必须正确保存初始 IRQL 值，并在函数退出时还原相同的 IRQL 值，这就是 **\_ irql \_ 要求 \_ 相同 \_** 的批注断言。

 

 





