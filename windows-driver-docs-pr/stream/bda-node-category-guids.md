---
title: BDA 节点类别 GUID
description: BDA 节点类别 GUID
ms.assetid: cf439881-d20d-4efc-8ea3-3752e117b14d
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8732ccab41d210a22b7169008d2e1500ea488c52
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386687"
---
# <a name="bda-node-category-guids"></a>BDA 节点类别 GUID


## <span id="ddk_bda_node_category_guids_ks"></span><span id="DDK_BDA_NODE_CATEGORY_GUIDS_KS"></span>


BDA 微型驱动程序使用 BDA 节点类别 Guid 来指定可用于创建 BDA 节点的类型。 BDA 微型驱动程序将分配其中一种 Guid 中的变量**类型**的成员[ **KSNODE\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksnode_descriptor)结构点。 *Bdamedia.h*标头文件定义了这些 Guid。

网络提供商使用 KSPROPERTY\_BDA\_节点\_类型的属性[KSPROPSETID\_BdaTopology](kspropsetid-bdatopology.md)属性设置为检索可从节点类型的列表BDA 微型驱动程序。 此节点类型列表是一个数组 KSNODE\_描述符结构。

以下节点类别 BDA 中提供了 Guid:

<span id="KSNODE_BDA_RF_TUNER"></span><span id="ksnode_bda_rf_tuner"></span>KSNODE\_BDA\_RF\_调谐器  
BDA 微型驱动程序将分配此 GUID 可实现： 电缆、 卫星或地面广播的 BDA 射频调谐器节点。

<span id="KSNODE_BDA_ANALOG_DEMODULATOR"></span><span id="ksnode_bda_analog_demodulator"></span>KSNODE\_BDA\_模拟\_解调器  
BDA 微型驱动程序将分配此 GUID 来指定 BDA 模拟类型解调器节点。

<span id="KSNODE_BDA_QAM_DEMODULATOR"></span><span id="ksnode_bda_qam_demodulator"></span>KSNODE\_BDA\_QAM\_DEMODULATOR  
BDA 微型驱动程序分配此 GUID 以 BDA QAM 类型解调器节点指定为数字视频广播 (DVB)-解调器电缆连接。

<span id="KSNODE_BDA_QPSK_DEMODULATOR"></span><span id="ksnode_bda_qpsk_demodulator"></span>KSNODE\_BDA\_QPSK\_DEMODULATOR  
BDA 微型驱动程序将分配此 GUID 指定 DVB 附属解调器 BDA QPSK 类型解调器节点。

<span id="KSNODE_BDA_8VSB_DEMODULATOR"></span><span id="ksnode_bda_8vsb_demodulator"></span>KSNODE\_BDA\_8VSB\_DEMODULATOR  
BDA 微型驱动程序分配此 GUID 来指定 BDA 8VSB 类型解调器节点用于高级电视系统委员会 (ATSC)-地面解调器。

<span id="KSNODE_BDA_COFDM_DEMODULATOR"></span><span id="ksnode_bda_cofdm_demodulator"></span>KSNODE\_BDA\_COFDM\_解调器  
BDA 微型驱动程序将分配此 GUID 指定 DVB 地面解调器 BDA COFDM 类型解调器节点。

<span id="KSNODE_BDA_OPENCABLE_POD"></span><span id="ksnode_bda_opencable_pod"></span>KSNODE\_BDA\_OPENCABLE\_POD  
BDA 微型驱动程序将分配此 GUID 来指定 BDA 开放电缆 POD 节点。

<span id="KSNODE_BDA_COMMON_CA_POD"></span><span id="ksnode_bda_common_ca_pod"></span>KSNODE\_BDA\_常见\_CA\_POD  
BDA 微型驱动程序将分配此 GUID 来指定 BDA 公共条件性访问 POD 节点。

<span id="KSNODE_BDA_PID_FILTER"></span><span id="ksnode_bda_pid_filter"></span>KSNODE\_BDA\_PID\_FILTER  
BDA 微型驱动程序将分配此 GUID 来指定 BDA 数据包标识符 (PID) 筛选器节点。

<span id="KSNODE_BDA_IP_SINK"></span><span id="ksnode_bda_ip_sink"></span>KSNODE\_BDA\_IP\_接收器  
BDA 微型驱动程序将此 GUID 来指定 BDA IP 分配汇聚节点。

<span id="KSNODE_BDA_ISDB_T_DEMODULATOR"></span><span id="ksnode_bda_isdb_t_demodulator"></span>KSNODE\_BDA\_ISDB\_T\_DEMODULATOR  
BDA 微型驱动程序将分配此 GUID 指定 DVB 地面解调器 BDA ISDB 类型解调器节点。

<span id="KSNODE_BDA_ISDB_S_DEMODULATOR"></span><span id="ksnode_bda_isdb_s_demodulator"></span>KSNODE\_BDA\_ISDB\_S\_DEMODULATOR  
BDA 微型驱动程序将分配此 GUID 指定 DVB 附属解调器 BDA ISDB 类型解调器节点。

 

 





