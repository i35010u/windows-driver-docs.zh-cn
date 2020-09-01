---
title: 添加 HelpText 值
description: 添加 HelpText 值
ms.assetid: fb29852c-5d47-4660-9fe4-dc8ae05449ff
keywords:
- 添加-注册表-"WDK 网络，HelpText" 值
- HelpText 值 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 318f2e4a10ff6b80f0575aa3bd5870bc839a27c8
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210791"
---
# <a name="adding-a-helptext-value"></a>添加 HelpText 值





在用户界面中可见的 **NetTrans**、 **NetClient**或 **空间** 网络组件的 INF 文件应将 **HelpText** 值 (REG \_ SZ) 添加到组件的 **Ndi** 键。

**请注意**，  **NetClient**组件在 Windows 8.1、Windows Server 2012 R2 和更高版本中已弃用。

 

**HelpText**值是一个可本地化的字符串，用于说明组件如何为用户带来好处。 例如， **NetClient**组件的**HelpText**值不应简单地标识客户端，而应指示客户端允许用户连接到的内容。 选择页面上的组件时， **HelpText**值将显示在 "**连接属性**" 对话框的 "**常规**" 页的底部。

**注意**    (适配器的网络组件) 和 IrDA 组件不支持**HelpText**值。

 

下面是将**HelpText**值添加到**Ndi**项的 "*添加注册表" 部分*的示例：

```INF
[MS_Protocol.ndi_reg]
HKR, Ndi, HelpText, 0, %MyTransport_Help%
```

**HelpText**值是在 INF 文件的**字符串**部分中定义的% *strkey*% 令牌。 有关 **字符串** 部分的详细信息，请参阅 [**INF 字符串部分**](../install/inf-strings-section.md)。

**注意**   对于多语言用户界面 (MUI) 支持， **HelpText**值可以是格式为的间接字符串 `@filename,resource` 。 例如： "@% SystemRoot% \\ System32 \\ 驱动程序 \\mydriver.sys，-1000"。 目标字符串位于指定的文件中。 资源值标识文件中的特定字符串。 如果资源值为零或更大，则将该数字用作二进制文件中的字符串的索引。 如果资源值为负数，则将其用作资源文件中的资源标识符。

 

 

