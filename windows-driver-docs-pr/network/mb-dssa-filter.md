---
title: DSSA 日志筛选器
description: DSSA 的 TextAnalysisTool 筛选器
ms.assetid: 4d575360-e867-4025-bb7d-575e1795c7e5
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: 343d5c9327d07f1eb4dbf26c3d58c81487467cee
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102250504"
---
# <a name="dssa-log-filter"></a>DSSA 日志筛选器

为了使搜索日志文件更简单，下面是 [TextAnalysisTool](https://github.com/TextAnalysisTool/Releases)的 DSSA 筛选器文件。 

使用 DSSA 日志筛选器： 

1. 复制并粘贴以下行，并将其保存到名为 "esimdownload. tat" 的文本文件中。

```
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<TextAnalysisTool.NET version="2016-06-16" showOnlyFilteredLines="True">
  <filters>
    <filter enabled="y" excluding="n" description="" backColor="add8e6" type="matches_text" case_sensitive="n" regex="n" text="[WwanDimCommon]QUERY OID_WWAN_DEVICE_CAPS_EX" />
    <filter enabled="y" excluding="n" description="" backColor="ffb6c1" type="matches_text" case_sensitive="n" regex="n" text="[WwanDimCommon]  StatusCode  : NDIS_STATUS_WWAN_DEVICE_SLOT" />
    <filter enabled="y" excluding="n" description="" backColor="f0e68c" type="matches_text" case_sensitive="n" regex="n" text="SET OID_WWAN_SYS_SLOTMAPPINGS" />
    <filter enabled="y" excluding="n" description="" backColor="90ee90" type="matches_text" case_sensitive="n" regex="n" text="[WwanDimCommon]QUERY OID_WWAN_SYS_CAPS" />
    <filter enabled="y" excluding="n" description="" backColor="ffb6c1" type="matches_text" case_sensitive="n" regex="n" text="[WwanDimCommon]      Executor Index" />
    <filter enabled="y" excluding="n" description="" backColor="add8e6" type="matches_text" case_sensitive="n" regex="n" text="CAPS_MULTI_SIM" />
    <filter enabled="y" excluding="n" description="" backColor="f08080" type="matches_text" case_sensitive="n" regex="n" text="[WwanDimCommon]  StatusCode  : NDIS_STATUS_WWAN_SLOT_INFO" />
    <filter enabled="y" excluding="n" description="" backColor="f08080" type="matches_text" case_sensitive="n" regex="n" text="[WwanDimCommon]  SlotState" />
    <filter enabled="y" excluding="n" description="" backColor="90ee90" type="matches_text" case_sensitive="n" regex="n" text="[WwanDimCommon]  StatusCode  : NDIS_STATUS_WWAN_SYS_CAPS_INFO" />
    <filter enabled="y" excluding="n" description="" backColor="90ee90" type="matches_text" case_sensitive="n" regex="n" text="[WwanDimCommon]  NumberOfExecutors" />
    <filter enabled="y" excluding="n" description="" backColor="90ee90" type="matches_text" case_sensitive="n" regex="n" text="[WwanDimCommon]  NumberOfSlots" />
    <filter enabled="n" excluding="n" description="" backColor="afeeee" type="matches_text" case_sensitive="n" regex="n" text="[WwanDimCommon]  ReadyState" />
    <filter enabled="y" excluding="n" description="" backColor="add8e6" type="matches_text" case_sensitive="n" regex="n" text="[WwanDimCommon]  StatusCode  : NDIS_STATUS_WWAN_DEVICE_CAPS_EX" />
    <filter enabled="y" excluding="n" description="" backColor="f0e68c" type="matches_text" case_sensitive="n" regex="n" text="[WwanDimCommon]  SlotMapListHeader" />
    <filter enabled="y" excluding="n" description="" backColor="f0e68c" type="matches_text" case_sensitive="n" regex="n" text="[WwanDimCommon]  Executor Index" />
    <filter enabled="y" excluding="n" description="" backColor="f08080" type="matches_text" case_sensitive="n" regex="n" text="[WwanDimCommon]  SlotIndex" />
    <filter enabled="y" excluding="n" description="" backColor="dda0dd" type="matches_text" case_sensitive="n" regex="n" text="[WwanDimCommon]QUERY OID_WWAN_SYS_SLOTMAPPINGS" />
    <filter enabled="y" excluding="n" description="" backColor="dcdcdc" type="matches_text" case_sensitive="n" regex="n" text="[WwanDimCommon]QUERY OID_WWAN_SLOT_INFO_STATUS" />
    <filter enabled="y" excluding="n" description="" backColor="d3d3d3" type="matches_text" case_sensitive="n" regex="n" text="[WwanDimCommon]  Slot Index" />
  </filters>
</TextAnalysisTool.NET>
```

2.  通过单击 "文件 > 加载筛选器将筛选器文件加载到 TextAnalysisTool 中。