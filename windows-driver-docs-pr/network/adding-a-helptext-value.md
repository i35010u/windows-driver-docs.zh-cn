---
title: 添加 HelpText 值
description: 添加 HelpText 值
ms.assetid: fb29852c-5d47-4660-9fe4-dc8ae05449ff
keywords:
- 添加注册表部分 WDK 网络 HelpText 值
- HelpText 值 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0573a425ae6b2f68cff26c78b40c2f5fbaa18be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367852"
---
# <a name="adding-a-helptext-value"></a>添加 HelpText 值





INF 文件**NetTrans**， **NetClient**，或**NetService**用户界面中是可见的网络组件应添加**HelpText**值 (REG\_SZ) 到组件的**Ndi**密钥。

**请注意**  **NetClient**组件在 Windows 8.1，Windows Server 2012 R2 中已弃用及更高版本。

 

**HelpText**值是可本地化的字符串说明该组件如何受益的用户。 例如， **HelpText**值**NetClient**组件不应只需标识客户端，但指示客户端所允许的用户连接到。 **HelpText**值显示在底部**常规**页**连接属性**时页面上的组件的对话框中选定了。

**请注意**  Net 组件 （适配器） 和 IrDA 组件不支持**HelpText**值。

 

以下是一种*添加注册表部分*，它将**HelpText**值设为**Ndi**密钥：

```INF
[MS_Protocol.ndi_reg]
HKR, Ndi, HelpText, 0, %MyTransport_Help%
```

**HelpText**值是 % *strkey*中定义的 %令牌**字符串**INF 文件部分。 有关详细信息**字符串**部分中，请参阅[ **INF 字符串部分**](https://msdn.microsoft.com/library/windows/hardware/ff547485)。

**请注意**  多语言用户界面 (MUI) 支持**HelpText**值可以是间接字符串形式`@filename,resource`。 例如:"@%SystemRoot %\\System32\\驱动程序\\mydriver.sys，-1000年"。 目标字符串位于指定的文件中。 资源值标识文件中的特定字符串。 如果资源值为零或更高版本的二进制文件中的字符串的索引使用数。 如果资源值为负，则将它用作资源文件中的资源标识符。

 

 

 





