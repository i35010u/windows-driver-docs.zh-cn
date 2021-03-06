---
title: eSIM 下载并安装日志筛选器
description: 适用于 eSIM 下载和安装的 TextAnalysisTool 筛选器
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: 458c6e6c761dd3d46c03b87b97ecaa433d19185c
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102250502"
---
# <a name="esim-download-and-install-log-filter"></a>eSIM 下载并安装日志筛选器

为了使搜索日志文件更简单，下面是 [TextAnalysisTool](https://github.com/TextAnalysisTool/Releases)的 eSIM 下载和安装筛选器文件。 

使用 eSIM 下载并安装日志筛选器：

1. 复制并粘贴以下行，并将其保存到名为 "esimdownload. tat" 的文本文件中。 

```
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<TextAnalysisTool.NET version="2015-08-17" showOnlyFilteredLines="True">
  <filters>
    <filter enabled="y" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="RpcDownloadProfile" />
    <filter enabled="y" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="LuiAsyncResult" />
    <filter enabled="y" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="DownloadSequenceEvent" />
  </filters>
</TextAnalysisTool.NET>
```

2. 通过单击 "文件 > 加载筛选器将筛选器文件加载到 TextAnalysisTool 中。