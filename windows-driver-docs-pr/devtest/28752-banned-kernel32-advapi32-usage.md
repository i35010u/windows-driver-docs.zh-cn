---
title: C28752
description: 警告 C28752 禁止使用 kernel32.dll 或 advapi32.dll API。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28752
ms.openlocfilehash: 9ee1fd6b68ef63272f9b54262a339dc893175b8a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788755"
---
# <a name="c28752"></a>C28752


警告 C28752： kernel32.dll 或 advapi32.dll API 的禁止使用

此警告意味着使用的函数已被弃用，并且具有作为核心系统的一部分的首选替换。

核心系统二进制文件提供了 kernel32.dll 和 advapi32.dll 所需的大部分功能，但在许多情况下，需要执行不同的 API 调用。 调用核心系统 Api 的速度更快，需要的内存占用量要小于调用旧的 kernel32.dll 或 advapi32.dll Api。

 

 





