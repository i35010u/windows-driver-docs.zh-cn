---
title: C28752
description: 警告的 kernel32 或 advapi32 API C28752 禁止使用情况。
ms.assetid: F887EB9E-FA5A-4139-AF67-7460BB9254B8
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28752
ms.openlocfilehash: fad7a7e4a6751f0f5a485e377686727935a8cbc3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545946"
---
# <a name="c28752"></a>C28752


警告 C28752:已禁止的 kernel32 或 advapi32 API 的用法

此警告意味着，正在使用的函数已被弃用，并且具有是核心系统的一部分的首选的替换。

核心系统二进制文件提供的众多功能 kernel32 和 advapi32 执行操作，但在许多情况下，不同的 API 调用是必需。 调用核心系统 Api 更快，并且需要较小的内存需求量比调用旧 kernel32 或 advapi32 Api。

 

 





