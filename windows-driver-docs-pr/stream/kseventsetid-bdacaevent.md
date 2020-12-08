---
title: KSEVENTSETID \_ BdaCAEvent
description: KSEVENTSETID \_ BdaCAEvent
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c0473c8c2d8b69f3e2accdd72da1447c5987ce7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815819"
---
# <a name="kseventsetid_bdacaevent"></a>KSEVENTSETID \_ BdaCAEvent


## <span id="ddk_kseventsetid_bdacaevent_ks"></span><span id="DDK_KSEVENTSETID_BDACAEVENT_KS"></span>


KSEVENTSETID \_ BdaCAEvent 是 (CA) 事件集的 BDA 条件性访问。 它用于通知 CA 插件与 (ECM) 映射节点的授权控制消息相关联的 CA 模块和智能卡读取器的状态更改。 此事件集还可以通知 CA 插件是否存在用户界面 (UI) 这些插件应检索和显示的信息以及有关程序信息的更改。

可用事件如下：

<span id="KSEVENT_BDA_PROGRAM_FLOW_STATUS_CHANGED"></span><span id="ksevent_bda_program_flow_status_changed"></span>[**KSEVENT \_ BDA \_ 程序 \_ 流 \_ 状态 \_ 已更改**](ksevent-bda-program-flow-status-changed.md)  
在程序信息中通知状态更改。

<span id="KSEVENT_BDA_CA_MODULE_STATUS_CHANGED"></span><span id="ksevent_bda_ca_module_status_changed"></span>[**KSEVENT \_ BDA \_ CA \_ 模块 \_ 状态 \_ 已更改**](ksevent-bda-ca-module-status-changed.md)  
与 ECM 映射节点关联的 CA 模块上的状态更改通知。

<span id="KSEVENT_BDA_CA_SMART_CARD_STATUS_CHANGED"></span><span id="ksevent_bda_ca_smart_card_status_changed"></span>[**KSEVENT \_ BDA \_ CA \_ 智能 \_ 卡 \_ 状态 \_ 已更改**](ksevent-bda-ca-smart-card-status-changed.md)  
与 ECM 映射节点关联的智能卡读取器上的状态更改通知。

<span id="KSEVENT_BDA_CA_MODULE_UI_REQUESTED"></span><span id="ksevent_bda_ca_module_ui_requested"></span>[**KSEVENT \_ BDA \_ CA \_ 模块 \_ UI 已 \_ 请求**](ksevent-bda-ca-module-ui-requested.md)  
通知存在 CA 插件可以检索和显示的 UI。

### <a name="comments"></a>注释

此事件集中的每个事件都对应于 KSPROPSETID \_ BdaCA 属性集中的一个属性。 当出现 BDA 组件中的事件时，请求通知 CA 插件。 此事件集中的 BDA 微型驱动程序信号事件，用于通知 CA 插件。 然后，这些 CA 插件将在 KSPROPSETID BdaCA 中查询对应的属性 \_ 。 如果发生重大状态更改或与用户进行交互，则 BDA 微型驱动程序会通知这些事件。 BDA 微型驱动程序与用户交互，例如向用户显示一条消息，或与用户协商某个事务。 例如，当用户从智能卡读卡器中删除智能卡时，会发生重大状态更改。

### <a name="see-also"></a>另请参阅

[KSPROPSETID \_ BdaCA](kspropsetid-bdaca.md)

 

 





