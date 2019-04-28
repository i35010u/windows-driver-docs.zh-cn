---
title: 星号字符注释行说明符
description: 如果星号字符是一个命令的开头，然后在行的其余部分作为处理注释，即使分号后出现。
ms.assetid: 46f68e92-0758-49f2-82bb-bc4d25ddb641
keywords:
- 注释行标记
- 注释行说明符 Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- (Comment Line Specifier)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c0a9a87651019cf4524a81039f36b2a6b0921c10
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337072"
---
# <a name="-comment-line-specifier"></a>\* （注释行说明符）


如果星号 ( **\\***) 字符是一个命令，开始时则行的其余内容被视为注释，即使分号后出现。

```dbgcmd
    * [any text]
```

<a name="remarks"></a>备注
-------

**\\*** 等任何其他调试器命令分析标记。 因此，如果你想要创建另一个命令后的注释，则必须在前面**\\*** 令牌以分号结尾。

**\\*** 令牌将导致该行被忽略的其余部分，即使分号后出现。 这不同于[ **$$ （注释说明符）**](-----comment-specifier-.md)，用于创建一条注释，可以由分号终止。

例如，以下命令将显示**eax**并**ebx**，但不是**ecx**:

```console
0:000> r eax; $$ some text; r ebx; * more text; r ecx 
```

文本加**\\*** 或[ **$$** ](-----comment-specifier-.md)令牌不以任何方式处理。 如果您在执行远程调试，在调试服务器中输入的注释将不会显示在调试客户端或进行相反转换。 如果你想要使应使用对所有参与方，可见的方式在调试器命令窗口中显示的注释文本[ **.echo （Echo 注释）**](-echo--echo-comment-.md)。

 

 





