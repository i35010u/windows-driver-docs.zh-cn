---
title: Hello World "定义文件
description: Hello World "定义文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2762c28227593b1b6753cee6fa0d11268e802983
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832983"
---
# <a name="hello-world-definition-file"></a>"Hello World" 定义文件

定义文件用于导出入口点函数。 *Hellowld* 文件应包含以下两个 COM 导出： **DllGetClassObject** 和 **DllCanUnloadNow**，如 Microsoft Windows SDK 文档中所述。

```make
LIBRARY HELLOWLD

EXPORTS
     DllGetClassObject   PRIVATE
     DllCanUnloadNow     PRIVATE
```
