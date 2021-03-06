---
title: 基本连接日志筛选器
description: 基本连接的 TextAnalysisTool 筛选器
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: c243910e6c51a037ad20c0e2a4ab1426a0f4773a
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102250427"
---
# <a name="basic-connectivity-log-filter"></a>基本连接日志筛选器

加载基本连接日志筛选器：

1. 复制并粘贴以下行，并将其保存到名为 "basicconnectivity. tat" 的文本文件中。 

2. 通过单击 "文件 > 加载筛选器将筛选器文件加载到 TextAnalysisTool 中。

```
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<TextAnalysisTool.NET version="2016-01-08" showOnlyFilteredLines="True">
  <filters>
    <filter enabled="y" excluding="n" description="" foreColor="800000" type="matches_text" case_sensitive="n" regex="n" text="Globals Module Initialization Completed" />
    <filter enabled="n" excluding="n" description="" foreColor="ff0000" type="matches_text" case_sensitive="n" regex="n" text="ERROR: " />
    <filter enabled="n" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="IsAutoConnectPossible" />
    <filter enabled="y" excluding="n" description="" foreColor="800080" type="matches_text" case_sensitive="n" regex="n" text="SetAcState" />
    <filter enabled="y" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="SetEnablementPolicy" />
    <filter enabled="y" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="SetRoamControlPolicy" />
    <filter enabled="n" excluding="n" description="" type="matches_text" case_sensitive="y" regex="n" text=": entry with state" />
    <filter enabled="n" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text=": exit with state" />
    <filter enabled="n" excluding="n" description="" foreColor="8b008b" type="matches_text" case_sensitive="n" regex="n" text=" Dispatch WwanNotificationSourceMsm\WwanMsmEventTypeConnectionIStream" />
    <filter enabled="y" excluding="n" description="" foreColor="006400" type="matches_text" case_sensitive="n" regex="n" text="OID_WWAN_CONNECT (" />
    <filter enabled="y" excluding="n" description="" foreColor="4b0082" type="matches_text" case_sensitive="n" regex="n" text=" Indicating NDIS_STATUS_WWAN_CONTEXT_STATE with status=" />
    <filter enabled="y" excluding="n" description="" foreColor="008b8b" type="matches_text" case_sensitive="n" regex="n" text="CWwanDataExecutor::OnNdisNotification: NDIS_STATUS_WWAN_CONTEXT_STATE Resp (" />
    <filter enabled="y" excluding="n" description="" foreColor="b22222" type="matches_text" case_sensitive="y" regex="n" text="BASIC_CONNECT" />
    <filter enabled="y" excluding="n" description="" foreColor="008080" type="matches_text" case_sensitive="n" regex="n" text="NDIS_STATUS_WWAN_CONTEXT_STATE Event" />
    <filter enabled="n" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="ound valid v" />
    <filter enabled="y" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="OnIPAddrLinkStateChange" />
    <filter enabled="n" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="WwanContextLifeCycleFSMState_Idle" />
    <filter enabled="n" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="WwanContextLifeCycleFSMState_Connected" />
    <filter enabled="y" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="data call connected" />
    <filter enabled="n" excluding="y" description="" type="matches_text" case_sensitive="n" regex="n" text="Qualcomm-WOS-mbb" />
    <filter enabled="n" excluding="n" description="" foreColor="00008b" type="matches_text" case_sensitive="n" regex="n" text="::OnNdisNotification: WwanEventCodeRegisterState" />
    <filter enabled="n" excluding="n" description="" foreColor="ff00ff" type="matches_text" case_sensitive="n" regex="n" text="::OnNdisNotification: WwanEventCodePacketService" />
    <filter enabled="n" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="-&gt;ActivOption DSResponse" />
    <filter enabled="n" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="-&gt;DataDormancyHint DSResponse" />
    <filter enabled="y" excluding="n" description="" foreColor="ff0000" type="matches_text" case_sensitive="n" regex="n" text="InternalErrorReport" />
    <filter enabled="y" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="ModemDualSIMCap" />
    <filter enabled="y" excluding="n" description="" foreColor="ff0000" type="matches_text" case_sensitive="n" regex="n" text="CWwanDataExecutorState::SendMbbPsAttachDetachReq" />
    <filter enabled="n" excluding="n" description="" foreColor="b22222" type="matches_text" case_sensitive="n" regex="n" text="WwanDefaultContextControllerFSMEvent_PSStateChanged" />
    <filter enabled="n" excluding="n" description="" foreColor="ff0000" type="matches_text" case_sensitive="n" regex="n" text="WwanDefaultContextControllerFSMEvent_ContextStoppedUnsolictedly" />
    <filter enabled="n" excluding="n" description="" foreColor="ff0000" type="matches_text" case_sensitive="n" regex="n" text="lossing link state or IP addr" />
    <filter enabled="n" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="_debouncing" />
    <filter enabled="n" excluding="n" description="" foreColor="ff0000" type="matches_text" case_sensitive="n" regex="n" text=" unsolicitedlt deactivated. APN " />
    <filter enabled="n" excluding="n" description="" foreColor="ff1493" type="matches_text" case_sensitive="n" regex="n" text="ims status update received" />
    <filter enabled="y" excluding="n" description="" foreColor="800000" type="matches_text" case_sensitive="n" regex="n" text="RetryBackoffT" />
    <filter enabled="n" excluding="n" description="" foreColor="006400" type="matches_text" case_sensitive="n" regex="n" text="CWWANContextControllerBase::StartTimer:  " />
    <filter enabled="n" excluding="n" description="" foreColor="800080" type="matches_text" case_sensitive="n" regex="n" text="CWwanDefaultContextController::CalculateArmBackoffTimer" />
    <filter enabled="n" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="WwanProtDim" />
    <filter enabled="n" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="wmbclass" />
    <filter enabled="n" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="MBIM" />
    <filter enabled="n" excluding="n" description="" foreColor="808000" type="matches_text" case_sensitive="y" regex="n" text="CID " />
    <filter enabled="n" excluding="n" description="" foreColor="808000" type="matches_text" case_sensitive="n" regex="n" text="CID=" />
    <filter enabled="n" excluding="n" description="" type="matches_text" case_sensitive="n" regex="n" text="AdaptersAddresses" />
  </filters>
</TextAnalysisTool.NET>
```