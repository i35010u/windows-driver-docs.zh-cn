---
title: Hello World 定义文件
description: Hello World 定义文件
ms.assetid: 50c38eea-7826-44bb-9048-ce8e07ce3478
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d0e5b40bbfd32d4f8f469ff249e3078c33bc967
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522593"
---
# <a name="hello-world-definition-file"></a>Hello World 定义文件

定义文件用于导出入口点函数。 *Hellowld.def*文件应包含两个以下的 COM 导出**DllGetClassObject**并**DllCanUnloadNow**，Microsoft Windows SDK 中描述这些文档。

```make
LIBRARY HELLOWLD

EXPORTS
     DllGetClassObject   PRIVATE
     DllCanUnloadNow     PRIVATE
```
