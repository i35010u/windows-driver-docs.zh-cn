---
title: 个人信息交换 (.pfx) 文件
description: 个人信息交换 (.pfx) 文件
ms.assetid: 58849ccc-c86f-4c49-b848-8926febb5521
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47a5d9fe8dfa02ca0315bd4d8df204eaff27ef4b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391476"
---
# <a name="personal-information-exchange-pfx-files"></a>个人信息交换 (.pfx) 文件


若要使用的版本签名，软件发行者证书 (SPC) 和其专用和公共密钥，必须存储在个人信息交换 (。*pfx*) 文件。 但是，某些证书颁发机构 (Ca) 使用不同的文件格式来存储此数据。 例如，某些 Ca 将证书的私钥存储在私钥 (。*pvk*) 文件和存储证书和公钥 *.spc*或 *.cer*文件。

如果 CA 颁发 *.spc*中以非及其密钥 *.pfx*文件，您必须转换和存储中的文件 *.pfx*文件才可以为版本签名中使用。 [ **Pvk2Pfx** ](https://msdn.microsoft.com/library/windows/hardware/ff550672)工具用于执行此转换。

下面的命令行示例将转换 *.pvk*名为的文件*abc.pvk*和一个 *.spc*名为*abc.spc*到 *.pfx*名为的文件*abc.pfx*:

```cpp
Pvk2Pfx -pvk abc.pvk -pi pvkpassword -spc abc.spc -pfx abc.pfx -po pfxpassword -f
```

其中：

-   **-Pvk**选项指定 *.pvk*文件 (*abc.pvk*)。

-   **-Pi**选项指定的密码。*pvk*文件 (*pvkpassword*)。

-   **-Spc**选项指定的名称和包含的证书的 SPC 文件扩展名。 该文件可以是 *.spc*文件或 *.cer*文件。 在此示例中，证书和公钥位于*abc.spc*文件。

-   **-Pfx**选项指定的名称 *.pfx*文件 (*abc.pfx*)。 如果未指定此选项，Pvk2Pfx 打开导出的向导，并忽略-采购订单和-f 自变量。

-   **Po**选项指定的密码 *.pfx*文件 (*pfxpassword*)。 如果未指定此选项，指定 *.pfx*文件的分配相同的密码与指定关联 *.pvk*文件。

-   **-F**选项配置 Pvk2Pfx 要替换的现有 *.pfx*文件如果存在。

有关 SPCs 和他们管理的详细信息，请参阅[软件发布者证书 (SPC)](software-publisher-certificate.md)。

 

 





