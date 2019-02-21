---
title: KSPROPSETID\_BdaCA
description: KSPROPSETID\_BdaCA
ms.assetid: 2ceb54ff-f111-4cf7-8c8e-f9a4dce42d4e
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 790b4723cbffc05290e133012bc211f4bd822e74
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542313"
---
# <a name="kspropsetidbdaca"></a>KSPROPSETID\_BdaCA


## <span id="ddk_kspropsetid_bdaca_ks"></span><span id="DDK_KSPROPSETID_BDACA_KS"></span>


KSPROPSETID\_BdaCA 是 BDA 条件性访问 (CA) 属性集。 它用于查询授权控制消息 (ECM) 站点地图节点为这些节点的状态和关联的 CA 模块和智能卡读卡器的状态。 设置此属性还可以查询的用户界面 (UI) CA 插件可以显示和控制对通过 ECM 站点地图节点处理程序的访问。

可用属性如下：

<span id="KSPROPERTY_BDA_ECM_MAP_STATUS"></span><span id="ksproperty_bda_ecm_map_status"></span>[**KSPROPERTY\_BDA\_ECM\_映射\_状态**](ksproperty-bda-ecm-map-status.md)  
返回上 ECM 站点地图节点的状态。

<span id="KSPROPERTY_BDA_CA_MODULE_STATUS"></span><span id="ksproperty_bda_ca_module_status"></span>[**KSPROPERTY\_BDA\_CA\_模块\_状态**](ksproperty-bda-ca-module-status.md)  
返回与 ECM 映射节点关联的 CA 模块上的状态。

<span id="KSPROPERTY_BDA_CA_SMART_CARD_STATUS"></span><span id="ksproperty_bda_ca_smart_card_status"></span>[**KSPROPERTY\_BDA\_CA\_智能\_卡\_状态**](ksproperty-bda-ca-smart-card-status.md)  
返回上与 ECM 映射节点关联的智能卡读取器状态。

<span id="KSPROPERTY_BDA_CA_MODULE_UI"></span><span id="ksproperty_bda_ca_module_ui"></span>[**KSPROPERTY\_BDA\_CA\_模块\_UI**](ksproperty-bda-ca-module-ui.md)  
返回一个 CA 插件，可以显示的 UI。

<span id="KSPROPERTY_BDA_CA_SET_PROGRAM_PIDS"></span><span id="ksproperty_bda_ca_set_program_pids"></span>[**KSPROPERTY\_BDA\_CA\_SET\_PROGRAM\_PIDS**](ksproperty-bda-ca-set-program-pids.md)  
在特定的程序中设置数据包标识符的列表。

<span id="KSPROPERTY_BDA_CA_REMOVE_PROGRAM"></span><span id="ksproperty_bda_ca_remove_program"></span>[**KSPROPERTY\_BDA\_CA\_REMOVE\_PROGRAM**](ksproperty-bda-ca-remove-program.md)  
阻止特定程序访问。

### <a name="comments"></a>备注

属性中设置此属性对应于事件中 KSEVENTSETID\_BdaCAEvent 事件集。 BDA 微型驱动程序发出信号中设置通知 CA 插件此事件的事件。 这些 CA 插件然后查询 KSPROPSETID 中的相应属性\_BdaCA。 BDA 微型驱动程序通知这些事件或者每当发生重要的状态更改或与用户进行交互。 BDA 微型驱动程序与用户交互，例如，若要向用户显示一条消息，或协商与用户事务。 重要的状态更改时，例如，用户卸下智能卡从智能卡读卡器。

### <a name="see-also"></a>另请参阅

[KSEVENTSETID\_BdaCAEvent](kseventsetid-bdacaevent.md)

 

 





