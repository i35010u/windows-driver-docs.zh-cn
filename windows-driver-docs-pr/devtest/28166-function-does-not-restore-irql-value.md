---
title: C28166
description: 该函数不会还原为当前位于函数入口，并且是的值的 IRQL 警告 C28166 所需执行此操作。
ms.assetid: 5835b2e7-0a66-474c-ba1b-40618403075d
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28166
ms.openlocfilehash: 9dc1669174b62b0db36a441be971d9fef2b56405
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361328"
---
# <a name="c28166"></a>C28166


警告 C28166:该函数不会将 irql 恢复为当前位于函数入口和执行此操作所需的值。

此警告意味着某函数有 **\_IRQL\_需要\_相同\_** 批注，并且没有通过不是，请通过函数退出时，此函数至少一个路径还原到的驱动程序已运行位于函数入口 IRQL IRQL。

通常情况下，  **\_IRQL\_需要\_相同\_** 批注使用回调函数。

若要避免此警告，该驱动程序必须正确保存 IRQL 初始值和还原相同的 IRQL 值在函数退出时，这是什么 **\_IRQL\_需要\_相同\_** 断言的批注。

 

 





