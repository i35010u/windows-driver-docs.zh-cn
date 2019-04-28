---
title: KSEVENTSETID\_BdaCAEvent
description: KSEVENTSETID\_BdaCAEvent
ms.assetid: e748a8a1-9aa4-41da-8cc2-02beb89a8887
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dfbec8c4ca8ab6ea88ea93142f49a9312a92438
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329607"
---
# <a name="kseventsetidbdacaevent"></a>KSEVENTSETID\_BdaCAEvent


## <span id="ddk_kseventsetid_bdacaevent_ks"></span><span id="DDK_KSEVENTSETID_BDACAEVENT_KS"></span>


KSEVENTSETID\_BdaCAEvent 是 BDA 条件性访问 (CA) 事件集。 它用于通知 CA 插件中的 CA 模块和授权控制消息 (ECM) 站点地图节点与相关联的智能卡读卡器状态的更改。 此事件集还可以通知 CA 插件有关这些插件应检索和显示的用户界面 (UI) 存在以及程序信息中的更改。

都可以与以下事件：

<span id="KSEVENT_BDA_PROGRAM_FLOW_STATUS_CHANGED"></span><span id="ksevent_bda_program_flow_status_changed"></span>[**KSEVENT\_BDA\_程序\_流\_状态\_已更改**](ksevent-bda-program-flow-status-changed.md)  
通知程序信息的状态更改。

<span id="KSEVENT_BDA_CA_MODULE_STATUS_CHANGED"></span><span id="ksevent_bda_ca_module_status_changed"></span>[**KSEVENT\_BDA\_CA\_模块\_状态\_已更改**](ksevent-bda-ca-module-status-changed.md)  
ECM 站点地图节点与相关联的 CA 模块上的状态更改的通知。

<span id="KSEVENT_BDA_CA_SMART_CARD_STATUS_CHANGED"></span><span id="ksevent_bda_ca_smart_card_status_changed"></span>[**KSEVENT\_BDA\_CA\_智能\_卡\_状态\_已更改**](ksevent-bda-ca-smart-card-status-changed.md)  
ECM 站点地图节点与相关联的智能卡读卡器上的状态更改的通知。

<span id="KSEVENT_BDA_CA_MODULE_UI_REQUESTED"></span><span id="ksevent_bda_ca_module_ui_requested"></span>[**KSEVENT\_BDA\_CA\_MODULE\_UI\_REQUESTED**](ksevent-bda-ca-module-ui-requested.md)  
通知的 CA 插件可以检索和显示的 UI 存在。

### <a name="comments"></a>备注

在此事件集中的每个事件都对应于 KSPROPSETID 中的属性\_BdaCA 属性集。 CA 插件的请求 BDA 组件中的事件发生时接收通知。 BDA 微型驱动程序发出信号中设置通知 CA 插件此事件的事件。 这些 CA 插件然后查询 KSPROPSETID 中的相应属性\_BdaCA。 BDA 微型驱动程序通知这些事件或者每当发生重要的状态更改或与用户进行交互。 BDA 微型驱动程序与用户交互，例如，若要向用户显示一条消息，或协商与用户事务。 重要的状态更改时，例如，用户卸下智能卡从智能卡读卡器。

### <a name="see-also"></a>请参阅

[KSPROPSETID\_BdaCA](kspropsetid-bdaca.md)

 

 





