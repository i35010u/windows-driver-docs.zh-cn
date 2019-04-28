---
title: C28636
description: 警告从对 GetSecurityDescriptorOwner/组/Dacl/Sacl 的非分配指针上调用 LocalFree C28636。
ms.assetid: cad12c6c-5d65-4c5b-98fa-4e0fa9e75166
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28636
ms.openlocfilehash: df20050c95648d23215b283cd4e7cb22056d0877
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347052"
---
# <a name="c28636"></a>C28636


警告 C28636:从对 GetSecurityDescriptorOwner/组/Dacl/Sacl 的非分配指针上调用 LocalFree

这些函数不分配任何内存 — 它们设置在传递的指针。 出于此原因，是错误的可用内存使用该指针。

 

 





