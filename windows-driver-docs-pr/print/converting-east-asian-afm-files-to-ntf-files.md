---
title: 将东亚版 AFM 文件转换为 NTF 文件
description: 将东亚版 AFM 文件转换为 NTF 文件
keywords:
- 微型驱动程序 WDK Pscript，转换 AFM 文件
- CONTOSO.NTF 文件
- contoso.ntf 文件
- afm 文件
- AFM 文件
- 将 AFM 文件转换为 CONTOSO.NTF 文件 WDK Pscript
- Adobe 字体指标 WDK Pscript
- 东亚字体 WDK 打印
- 亚洲字体 WDK 打印
- 简体中文支持 WDK 打印
- 中文传统字体支持 WDK 打印
- 日语支持 WDK
- 朝鲜语字体支持 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c33441a9ee657a46af0c953d68b7202dc48155a6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797505"
---
# <a name="converting-east-asian-afm-files-to-ntf-files"></a>将东亚版 AFM 文件转换为 NTF 文件





若要处理东亚字体的 afm 文件，请 Makentf.exe (将 [Afm 文件转换为 Contoso.ntf 文件](converting-afm-files-to-ntf-files.md) 中所述的) 需要使用映射和 .ps 文件创建从 UNICODE 到 CID 的映射表 (字体的字符 ID) 。

东亚的 afm 文件包含字体中包含的每个字形的 CID 说明和指标。 .Map 文件列出字体字符集的 Unicode 代码和对应的字符代码。 .Ps 文件包含 Unicode 代码列表和该字体字符集的相应 Cid。

从东亚的 afm 文件开始，Makentf.exe 确定字符集。 根据字符集，Makentf.exe 将查找适当的 .map 和 .ps 文件。 在 .map 文件中，Makentf.exe 列出了可用于字体的 Unicode 代码。 从 Unicode 代码列表和 .ps 文件中，Makentf.exe 然后创建该字体的 Unicode 到 CID 的映射表。 目前，此文件用于验证每个 CID (标志符号) 是否确实包含在该字体中。 如果在该文件中找到了该 CID，则会在映射表中创建从 Unicode 代码到 CID 的映射条目。 如果找不到该 CID，则不会创建映射条目。

以下列表显示了为简体中文、繁体中文、日语和朝鲜语创建 contoso.ntf 文件所需的 .map 和 .ps 文件。 将这些文件和你的 afm 文件放在同一目录中。

### <a name="chinese-simplified"></a>简体中文

-   ucs2gbk

-   unigbh.ps

-   unigbv.ps

### <a name="chinese-traditional"></a>中文(繁体)

-   ucs2bg5

-   unicnsh.ps

-   unicnsv.ps

### <a name="japanese"></a>日语

-   ucs283h

-   ucs283v

-   ucs2msj

-   uni83h.ps

-   uni83v.ps

-   unijish.ps

-   unijisv.ps

### <a name="korean"></a>韩语

-   ucs2jhb

-   ucs2uhc

-   uniksh.ps

-   uniksv.ps

 

 




