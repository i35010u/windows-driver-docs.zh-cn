---
title: C28625
description: 将优化掉用于清除敏感数据的警告 C28625 函数调用。
ms.assetid: 9ae44fbc-9a56-41e4-9972-d76d9b62033c
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28625
ms.openlocfilehash: 49384914d5f3f3f3f834d5eba57ace3743e0cfd1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540412"
---
# <a name="c28625"></a>C28625


警告 C28625:将优化掉用于清除敏感数据的函数调用

当前函数调用可能会在编译期间，这可能使敏感数据保留在内存中进行优化。 使用**SecureZeroMemory**或**RtlSecureZeroMemory**函数。 启发式方法查找的标识符名称包含诸如"密钥"或"通过"以触发此警告。

 

 





