---
title: C28625
description: 警告 C28625 用于清除敏感数据的函数调用将被优化掉。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28625
ms.openlocfilehash: 22df476503f0a751a4789fc446de27d9ebb776aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793125"
---
# <a name="c28625"></a>C28625


警告 C28625：用于清除敏感数据的函数调用将被优化掉

在编译过程中，可能会对当前函数调用进行优化，这可能会导致敏感数据保留在内存中。 改为使用 **SecureZeroMemory** 或 **RtlSecureZeroMemory** 函数。 试探法查找包含项（如 "key" 或 "pass"）的标识符名称以触发此警告。

 

 





