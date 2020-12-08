---
title: KSPROPSETID \_ BdaCA
description: KSPROPSETID \_ BdaCA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfebff54e8b27e58e29b1025b56b9e717cb93ba4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811347"
---
# <a name="kspropsetid_bdaca"></a>KSPROPSETID \_ BdaCA


## <span id="ddk_kspropsetid_bdaca_ks"></span><span id="DDK_KSPROPSETID_BDACA_KS"></span>


KSPROPSETID \_ BdaCA 是 (CA) 属性集的 BDA 条件访问。 它用于查询授权控制消息 (ECM) 映射节点以了解这些节点的状态以及关联的 CA 模块和智能卡读卡器的状态。 此属性集还可以查询用户界面 (UI) CA 插件可以显示和控制对通过 ECM 映射节点处理的程序的访问。

以下属性可用：

<span id="KSPROPERTY_BDA_ECM_MAP_STATUS"></span><span id="ksproperty_bda_ecm_map_status"></span>[**KSPROPERTY \_ BDA \_ ECM \_ 映射 \_ 状态**](ksproperty-bda-ecm-map-status.md)  
返回 ECM 映射节点上的状态。

<span id="KSPROPERTY_BDA_CA_MODULE_STATUS"></span><span id="ksproperty_bda_ca_module_status"></span>[**KSPROPERTY \_ BDA \_ CA \_ 模块 \_ 状态**](ksproperty-bda-ca-module-status.md)  
返回与 ECM 映射节点关联的 CA 模块上的状态。

<span id="KSPROPERTY_BDA_CA_SMART_CARD_STATUS"></span><span id="ksproperty_bda_ca_smart_card_status"></span>[**KSPROPERTY \_ BDA \_ CA \_ 智能 \_ 卡 \_ 状态**](ksproperty-bda-ca-smart-card-status.md)  
返回与 ECM 映射节点关联的智能卡读取器的状态。

<span id="KSPROPERTY_BDA_CA_MODULE_UI"></span><span id="ksproperty_bda_ca_module_ui"></span>[**KSPROPERTY \_ BDA \_ CA \_ 模块 \_ UI**](ksproperty-bda-ca-module-ui.md)  
返回某个 CA 插件可以显示的 UI。

<span id="KSPROPERTY_BDA_CA_SET_PROGRAM_PIDS"></span><span id="ksproperty_bda_ca_set_program_pids"></span>[**KSPROPERTY \_ BDA \_ CA \_ SET \_ PROGRAM \_ PID**](ksproperty-bda-ca-set-program-pids.md)  
在特定程序中设置数据包标识符的列表。

<span id="KSPROPERTY_BDA_CA_REMOVE_PROGRAM"></span><span id="ksproperty_bda_ca_remove_program"></span>[**KSPROPERTY \_ BDA \_ CA \_ 删除 \_ 程序**](ksproperty-bda-ca-remove-program.md)  
阻止访问特定程序。

### <a name="comments"></a>注释

此属性集中的属性对应于 KSEVENTSETID \_ BdaCAEvent 事件集中的事件。 此事件集中的 BDA 微型驱动程序信号事件，用于通知 CA 插件。 然后，这些 CA 插件将在 KSPROPSETID BdaCA 中查询对应的属性 \_ 。 如果发生重大状态更改或与用户进行交互，则 BDA 微型驱动程序会通知这些事件。 BDA 微型驱动程序与用户交互，例如向用户显示一条消息，或与用户协商某个事务。 例如，当用户从智能卡读卡器中删除智能卡时，会发生重大状态更改。

### <a name="see-also"></a>另请参阅

[KSEVENTSETID \_ BdaCAEvent](kseventsetid-bdacaevent.md)

 

 





