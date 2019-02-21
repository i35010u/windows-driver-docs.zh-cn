---
title: 将东亚 AFM 文件转换为 NTF 文件
description: 将东亚 AFM 文件转换为 NTF 文件
ms.assetid: 0932068a-9101-4cdc-8c80-b2d3a4b507ba
keywords:
- 微型驱动程序 WDK Pscript，转换 AFM 文件
- NTF 文件
- .ntf 文件
- .afm 文件
- AFM 文件
- 将 AFM 文件转换为 NTF 文件 WDK Pscript
- Adobe 字体指标 WDK Pscript
- 东亚字体 WDK 打印
- 亚洲字体 WDK 打印
- 简体中文字体支持 WDK 打印
- 繁体中文字体支持 WDK 打印
- 日语字体支持 WDK
- 朝鲜语字体支持 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef9272459d5353a20f2273779bb596627aeb207e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523452"
---
# <a name="converting-east-asian-afm-files-to-ntf-files"></a>将东亚 AFM 文件转换为 NTF 文件





若要处理东亚字体.afm 文件，Makentf.exe (中所述[NTF 文件转换 AFM 文件](converting-afm-files-to-ntf-files.md)) 需要.map 和.ps 文件，以创建映射表从 Unicode 到 CID (字符 ID) 的字体。

东亚.afm 文件具有 CID 说明和该字体中包含每个字形的指标。 .Map 文件列出了 Unicode 代码和相应的字体的字符集的字符代码。 .Ps 文件包含 Unicode 代码的列表和字体的字符的相应 Cid 设置。

从开始使用东亚.afm 文件，Makentf.exe 决定该字符集。 基于的字符集，Makentf.exe 查找相应的.map 和.ps 文件。 从.map 文件 Makentf.exe 列出了可以使用该字体中的 Unicode 代码。 从 Unicode 代码列表和.ps 文件，Makentf.exe 然后创建该字体的 Unicode CID 映射表。 目前，.afm 文件用于验证该字体中实际包含每个 CID （标志符号）。 如果.afm 文件中找到 CID，则在映射表中创建从 Unicode 代码到 CID 一个映射条目。 如果找不到 CID，不创建映射项。

以下列表中显示为简体中文、 繁体中文、 日语和朝鲜语创建.ntf 文件所需的.map 和.ps 文件。 将这些文件和.afm 文件放在同一目录中。

### <a name="chinese-simplified"></a>简体中文

-   ucs2gbk.map

-   unigbh.ps

-   unigbv.ps

### <a name="chinese-traditional"></a>繁体中文

-   ucs2bg5.map

-   unicnsh.ps

-   unicnsv.ps

### <a name="japanese"></a>日语

-   ucs283h.map

-   ucs283v.map

-   ucs2msj.map

-   uni83h.ps

-   uni83v.ps

-   unijish.ps

-   unijisv.ps

### <a name="korean"></a>朝鲜语

-   ucs2jhb.map

-   ucs2uhc.map

-   uniksh.ps

-   uniksv.ps

 

 




