---
title: C28157
description: 警告 C28157 IRQL 从未恢复。
ms.assetid: 3c60253f-5d89-4bb7-9787-9a2aa42bf7fb
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28157
ms.openlocfilehash: 1314dab061dfe7c82dba8a4f7e17c2e5f00fb79e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561956"
---
# <a name="c28157"></a>C28157


警告 C28157:IRQL 从未恢复

当前函数具有 **\_IRQL\_还原\_** 批注，这要求，操作完成时，该驱动程序应在执行之前的 IRQL 值已还原的 IRQL。 但是，没有至少一个驱动程序正在其中执行不同的 IRQL 在函数完成时的路径。

 

 





