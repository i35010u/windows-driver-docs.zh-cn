---
title: C28640
description: 警告 C28640 函数延迟加载存根应为静态函数。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28640
ms.openlocfilehash: 7b49aa5b1ed3d8628dea6eac11985dddca90cd74
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819799"
---
# <a name="c28640"></a>C28640


警告 C28640：函数延迟加载存根应为静态函数

所有延迟加载库应为静态的;它们不应具有符号导出。 这可确保没有任何意外软件可以链接到延迟加载存根（stub）函数。 如果未遵循此准则，则二进制可能会公开可能会被不当使用的导出。

 

 





