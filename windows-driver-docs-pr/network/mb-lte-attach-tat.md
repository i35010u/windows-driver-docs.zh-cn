---
title: LTE 附加操作日志筛选器
description: LTE 附加操作的 TextAnalysisTool 筛选器
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: 6ed23dd01f6f2e33413b5847912d649fe6d9f475
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102250537"
---
# <a name="lte-attach-log-filter"></a>LTE 附加日志筛选器

若要为 LTE 附加操作加载 [TextAnalysisTool](mb-analyzing-logs.md) 筛选器，请执行以下操作：

1. 复制并粘贴以下行，并将其保存到名为 "lte-attach. tat" 的文本文件中。 
1. 通过单击 "文件 > 加载筛选器将筛选器文件加载到 TextAnalysisTool 中。

```
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<TextAnalysisTool.NET version="2014-04-22" showOnlyFilteredLines="True">
  <filters>
    <filter enabled="y" excluding="n" type="matches_text" case_sensitive="n" regex="n" text="SaveModemConfiguredLteAttachConfig" />
    <filter enabled="y" excluding="n" type="matches_text" case_sensitive="n" regex="n" text="[WwanProtDim] StatusCode : NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG (0x4004103d)" />
    <filter enabled="y" excluding="n" type="matches_text" case_sensitive="n" regex="n" text="WwanPmSetDMConfigProfile" />
    <filter enabled="y" excluding="n" type="matches_text" case_sensitive="n" regex="n" text="CWwanDataExecutor::OnLteAttachProfileUpdate" />
    <filter enabled="y" excluding="n" type="matches_text" case_sensitive="n" regex="n" text="ReadyState  : WwanReadyStateInitialized" />
    <filter enabled="y" excluding="n" color="ff0000" type="matches_text" case_sensitive="n" regex="n" text="WwanPmGetLteAttachProfileInEffect" />
    <filter enabled="y" excluding="n" color="0000ff" type="matches_text" case_sensitive="n" regex="n" text="IsSameLTEAttachAPN" />
    <filter enabled="y" excluding="n" type="matches_text" case_sensitive="n" regex="n" text="[WwanProtDim] ReadyState" />
    <filter enabled="n" excluding="n" type="matches_text" case_sensitive="n" regex="n" text="LTEAttachConfig" />
  </filters>
</TextAnalysisTool.NET>
```