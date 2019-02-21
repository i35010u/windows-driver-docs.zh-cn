---
title: $ $ （注释说明符）
description: 如果命令的开头显示两个美元符号 （$$），然后在行的其余部分被视为注释，除非由分号终止注释。
ms.assetid: bafd5e97-d443-4bfc-b3ee-c2867ed139a2
keywords:
- 注释标记 （$$）
- $$ （注释说明符） Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- $$ (Comment Specifier)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 63a5e0bd2db2ac7f6831b8023fcff2442d4f5217
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543323"
---
# <a name="-comment-specifier"></a>$ $ （注释说明符）


如果两个货币进行签名 ( **$$** ) 命令，开始时出现，则行的其余内容被视为注释，除非由分号终止注释。


   $ $ [任意文本]


<a name="remarks"></a>备注
-------

**$$** 像任何其他调试器命令分析标记。 因此，如果你想要创建另一个命令后的注释，则必须在前面**$$** 令牌以分号结尾。

**$$** 后它直到结束的行或直到遇到分号被忽略，令牌将会导致文本。 分号终止注释;作为标准命令解析分号后的文本。 这不同于[  **\* （注释行说明符）**](----comment-line-specifier-.md)，这使该行的其余部分为一条注释，即使存在分号。

例如，以下命令将显示**eax**并**ebx**，但不是**ecx**:

```console
0:000> r eax; $$ some text; r ebx; * more text; r ecx 
```

文本加[ **\\** * ](----comment-line-specifier-.md)或者**$$** 令牌不以任何方式处理。 如果您在执行远程调试，在调试服务器中输入的注释将不会显示在调试客户端或进行相反转换。 如果你想要使应使用对所有参与方，可见的方式在调试器命令窗口中显示的注释文本[ **.echo （Echo 注释）**](-echo--echo-comment-.md)。

 

 





