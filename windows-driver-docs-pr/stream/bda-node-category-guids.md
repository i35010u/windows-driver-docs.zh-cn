---
title: BDA 节点类别 GUID
description: BDA 节点类别 GUID
ms.assetid: cf439881-d20d-4efc-8ea3-3752e117b14d
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 004e6445876a041174bdfbf83aef7629b7d7fc3f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187422"
---
# <a name="bda-node-category-guids"></a>BDA 节点类别 GUID


## <span id="ddk_bda_node_category_guids_ks"></span><span id="DDK_BDA_NODE_CATEGORY_GUIDS_KS"></span>


BDA 微型驱动程序使用 BDA 节点类别 Guid 来指定可创建的 BDA 节点类型。 BDA 微型驱动程序将其中一个 Guid 分配给[**KSNODE \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksnode_descriptor)结构的**类型**成员指向的变量中。 *Bdamedia*头文件定义这些 guid。

网络提供程序使用 \_ \_ \_ [KSPROPSETID \_ BdaTopology](kspropsetid-bdatopology.md) 属性集的 KSPROPERTY BDA 节点类型属性来检索可从 BDA 微型驱动程序获取的节点类型的列表。 此节点类型列表是 KSNODE 描述符结构的数组 \_ 。

以下节点类别 Guid 可用于 BDA：

<span id="KSNODE_BDA_RF_TUNER"></span><span id="ksnode_bda_rf_tuner"></span>KSNODE \_ BDA \_ RF \_ 调谐器  
BDA 微型驱动程序分配此 GUID，为有线、卫星或地面广播指定 BDA 射频调谐器节点。

<span id="KSNODE_BDA_ANALOG_DEMODULATOR"></span><span id="ksnode_bda_analog_demodulator"></span>KSNODE \_ BDA \_ 模拟 \_ 解调器  
BDA 微型驱动程序分配此 GUID 来指定 BDA 模拟类型的解调器节点。

<span id="KSNODE_BDA_QAM_DEMODULATOR"></span><span id="ksnode_bda_qam_demodulator"></span>KSNODE \_ BDA \_ QAM \_ 解调器  
BDA 微型驱动程序分配此 GUID 以指定用于数字视频广播 (DVB) 的 QAM 的 demodulators 节点。

<span id="KSNODE_BDA_QPSK_DEMODULATOR"></span><span id="ksnode_bda_qpsk_demodulator"></span>KSNODE \_ BDA \_ QPSK \_ 解调器  
BDA 微型驱动程序分配此 GUID 为 DVB 卫星 demodulators 指定 BDA QPSK 类型的解调器节点。

<span id="KSNODE_BDA_8VSB_DEMODULATOR"></span><span id="ksnode_bda_8vsb_demodulator"></span>KSNODE \_ BDA \_ 8VSB \_ 解调器  
BDA 微型驱动程序将此 GUID 分配给高级电视系统委员会 (ATSC) -陆地 demodulators。

<span id="KSNODE_BDA_COFDM_DEMODULATOR"></span><span id="ksnode_bda_cofdm_demodulator"></span>KSNODE \_ BDA \_ COFDM \_ 解调器  
BDA 微型驱动程序分配此 GUID 为 DVB-陆地 demodulators 指定 BDA COFDM 类型的解调器节点。

<span id="KSNODE_BDA_OPENCABLE_POD"></span><span id="ksnode_bda_opencable_pod"></span>KSNODE \_ BDA \_ OPENCABLE \_ POD  
BDA 微型驱动程序分配此 GUID 来指定 BDA 的开放缆盒节点。

<span id="KSNODE_BDA_COMMON_CA_POD"></span><span id="ksnode_bda_common_ca_pod"></span>KSNODE \_ BDA \_ 公共 \_ CA \_ POD  
BDA 微型驱动程序分配此 GUID 来指定 BDA 公共条件访问 POD 节点。

<span id="KSNODE_BDA_PID_FILTER"></span><span id="ksnode_bda_pid_filter"></span>KSNODE \_ BDA \_ PID \_ 筛选器  
BDA 微型驱动程序将此 GUID 分配给 (PID) filter 节点指定 BDA 数据包标识符。

<span id="KSNODE_BDA_IP_SINK"></span><span id="ksnode_bda_ip_sink"></span>KSNODE \_ BDA \_ IP \_ 接收器  
BDA 微型驱动程序分配此 GUID 来指定 BDA IP 接收器节点。

<span id="KSNODE_BDA_ISDB_T_DEMODULATOR"></span><span id="ksnode_bda_isdb_t_demodulator"></span>KSNODE \_ BDA \_ ISDB \_ T \_ 解调器  
BDA 微型驱动程序分配此 GUID 为 DVB-陆地 demodulators 指定 BDA ISDB 类型的解调器节点。

<span id="KSNODE_BDA_ISDB_S_DEMODULATOR"></span><span id="ksnode_bda_isdb_s_demodulator"></span>KSNODE \_ BDA \_ ISDB \_ S \_ 解调器  
BDA 微型驱动程序分配此 GUID 为 DVB 卫星 demodulators 指定 BDA ISDB 类型的解调器节点。

 

