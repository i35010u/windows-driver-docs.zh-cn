---
title: C28640
description: 警告 C28640 函数延迟加载存根 （stub） 应该是一个静态函数。
ms.assetid: 7e4c675b-5f5c-461a-bf80-cd7ba0d8832c
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28640
ms.openlocfilehash: bda1348cb0f840a010fd006c427f1d894f8a93be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353115"
---
# <a name="c28640"></a>C28640


警告 C28640： 函数延迟加载存根 （stub） 应为静态函数

延迟加载的所有库应该都是静态的;它们应具有无符号的导出。 这可确保不意外的软件可以链接到延迟加载存根 （stub） 函数。 如果未遵循此原则，二进制文件可能会公开可能使用不当的导出。

 

 





