---
title: 个人信息交换 (.pfx) 文件
description: 个人信息交换 (.pfx) 文件
ms.assetid: 58849ccc-c86f-4c49-b848-8926febb5521
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf53a451872a79f2e1962ccbcabc48e6b2b23a7a
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096311"
---
# <a name="personal-information-exchange-pfx-files"></a>个人信息交换 (.pfx) 文件


要用于发布签名，软件发行者证书 (SPC) 及其私钥和公钥必须存储在个人信息交换 ( 中。*pfx*) 文件。 但是，某些证书颁发机构 (Ca) 使用不同的文件格式来存储此数据。 例如，某些 Ca 将证书的私钥存储在私钥 ( 中。*pvk*) 文件，并将证书和公钥存储在 *.spc* 或 *.cer* 文件中。

如果 CA 在非 *.pfx*文件中颁发了 *.spc*及其密钥，则必须先转换文件并将其存储在 *.pfx*文件中，然后才能将其用于发布签名。 [**Pvk2Pfx**](../devtest/pvk2pfx.md)工具用于执行此转换。

以下命令行示例将名为*pvk*的*pvk*文件和一个名*为 abc 的* *.spc*转换为一个名为*abc*的 *.pfx*文件：

```cpp
Pvk2Pfx -pvk abc.pvk -pi pvkpassword -spc abc.spc -pfx abc.pfx -po pfxpassword -f
```

其中：

-   **-Pvk**选项指定*pvk*文件 (*pvk*) 。

-   **-Pi**选项指定的密码。*pvk*文件 (*pvkpassword*) 。

-   **-Spc**选项指定包含证书的 spc 文件的名称和扩展名。 该文件可以是 *.spc* 文件或 *.cer* 文件。 在此示例中，证书和公钥位于 *abc .spc* 文件中。

-   **-Pfx**选项指定 *.pfx* *文件 (的名称) 。* 如果未指定此选项，Pvk2Pfx 将打开导出向导并忽略-po 和-f 参数。

-   **-Po**选项为 *.pfx*文件指定密码 (*pfxpassword*) 。 如果未指定此选项，则为指定的 *.pfx* 文件分配与指定的 *pvk* 文件相关联的相同密码。

-   **-F**选项将 Pvk2Pfx 配置为替换现有的 *.pfx*文件（如果存在）。

有关 SPCs 及其管理的详细信息，请参阅 [软件发行者证书 (SPC) ](software-publisher-certificate.md)。

 

