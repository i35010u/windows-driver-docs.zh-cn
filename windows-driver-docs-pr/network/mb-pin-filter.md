---
title: PIN 操作日志筛选器
description: 用于 PIN 操作的 TextAnalysisTool 筛选器
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: 766137173e563787f8195fa78c228213f2c80eef
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102250429"
---
# <a name="pin-operations-log-filter"></a>PIN 操作日志筛选器

为了使搜索日志文件更简单，下面是 [TextAnalysisTool](https://github.com/TextAnalysisTool/Releases)的特定于 PIN 操作的筛选器文件。 

使用此筛选器：
 
1. 复制并粘贴以下行，并将其保存到名为 "WwanPin. tat" 的文本文件中。 

2. 通过单击 "文件 > 加载筛选器将筛选器文件加载到 TextAnalysisTool 中。

```
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<TextAnalysisTool.NET version="2015-06-23" showOnlyFilteredLines="True">
  <filters>
    <filter enabled="n" excluding="n" backColor="90ee90" type="matches_text" case_sensitive="n" regex="n" text="maybeUnlockPin" />
    <filter enabled="n" excluding="n" foreColor="800000" type="matches_text" case_sensitive="n" regex="n" text="Received PinInfo" />
    <filter enabled="n" excluding="n" backColor="ffb6c1" type="matches_text" case_sensitive="n" regex="n" text="maybeCapturePin" />
    <filter enabled="n" excluding="n" foreColor="800080" type="matches_text" case_sensitive="n" regex="n" text="[Microsoft-Windows-WWAN-SVC-EVENTS]" />
    <filter enabled="n" excluding="n" foreColor="00008b" type="matches_text" case_sensitive="n" regex="n" text="PinAction" />
    <filter enabled="n" excluding="n" backColor="dda0dd" type="matches_text" case_sensitive="n" regex="n" text="tracePinDesc" />
    <filter enabled="n" excluding="n" foreColor="008000" type="matches_text" case_sensitive="n" regex="n" text="processPinInfoResponse" />
    <filter enabled="n" excluding="n" foreColor="0000ff" type="matches_text" case_sensitive="n" regex="n" text="processPinActionResponse" />
    <filter enabled="n" excluding="n" foreColor="dc143c" type="matches_text" case_sensitive="n" regex="n" text="processPinListResponse" />
    <filter enabled="n" excluding="n" type="matches_text" case_sensitive="n" regex="n" text="NDIS_STATUS_WWAN_PIN_INFO" />
  </filters>
</TextAnalysisTool.NET>
```