---
title: eSIM 配置文件操作日志筛选器
description: ESIM 配置文件操作的 TextAnalysisTool 筛选器
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: a8c471bb9ca72910745ec0ddb742e643c36dbe64
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102250436"
---
# <a name="esim-profile-operations-log-filter"></a>eSIM 配置文件操作日志筛选器

为了使搜索日志文件更简单，下面是 [TextAnalysisTool](https://github.com/TextAnalysisTool/Releases)的 eSIM 配置文件操作筛选器文件。 

使用 eSIM 配置文件操作日志筛选器：

1. 复制并粘贴以下行，并将其保存到名为 "esimoperation. tat" 的文本文件中。 此筛选器用于 "EnableProfile" 操作。 对于其他操作，请将 "RpcEnableProfile" 替换为以下特定于该操作的字符串之一。

```
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<TextAnalysisTool.NET version="2015-08-17" showOnlyFilteredLines="True">
  <filters>
    <filter enabled="y" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="RpcEnableProfile" />
    <filter enabled="y" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="OpenChannel" />
    <filter enabled="y" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="CloseChannel" />
    <filter enabled="y" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="CardResetComplete" />
    <filter enabled="y" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="LuiAsyncResult" />
    <filter enabled="y" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="WwapiEsimUpdate" />
    <filter enabled="y" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="SendApdu" />
  </filters>
</TextAnalysisTool.NET>
``` 

```
Enable Profile  - RpcEnableProfile
Disable Profile - RpcDisableProfile
Delete Profile  - RpcDeleteProfile
Set Nick Name   - RpcSetProfileNickname
Reset eSim      - RpcWipeEsim
```

2. 通过单击 "文件 > 加载筛选器将筛选器文件加载到 TextAnalysisTool 中。 

