---
title: C28636
description: 警告 C28636 对从调用 GetSecurityDescriptorOwner/Group/Dacl/Sacl 获取的非分配指针调用 LocalFree 时出现警告。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28636
ms.openlocfilehash: 63c0d76d2a3ab9f32589b08bf87e94ffcd8e90d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819819"
---
# <a name="c28636"></a>C28636


警告 C28636：在通过调用 GetSecurityDescriptorOwner/Group/Dacl/Sacl 获取的非分配指针上调用 LocalFree

这些函数不会分配任何内存，它们会设置传入的指针。 出于此原因，使用该指针的内存释放是错误的。

 

 





