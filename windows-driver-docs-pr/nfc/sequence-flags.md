---
title: 序列标志
description: NFC CX 为序列事件定义以下常量。
ms.assetid: AC6CE286-52F7-4FC9-9F38-CD10C1413A90
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
topic_type:
- apiref
api_name:
- NFC_CX_SEQUENCE_PRE_INIT_FLAG_SKIP_CONFIG
- NFC_CX_SEQUENCE_PRE_INIT_FLAG_FORCE_CONFIG
- NFC_CX_SEQUENCE_INIT_COMPLETE_FLAG_REDO
- NFC_CX_SEQUENCE_PRE_NFCEE_DISC_FLAG_SKIP
- NFC_CX_SEQUENCE_PRE_SHUTDOWN_FLAG_SKIP_RESET
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45f393c9737e1184e6895883fe2fcba4d3797c38
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834003"
---
# <a name="sequence-flags"></a>序列标志


NFC CX 为序列事件定义以下常量。


### <a name="nfc_cx_sequence_pre_init_flag_skip_config"></a>NFC\_CX\_序列\_预\_INIT\_标志\_跳过\_配置

0x00000001

此标志在预初始化序列中用于在 NCI 初始化后跳过配置更新。 请注意，此标志不能与 force 配置选项一起使用。

### <a name="nfc_cx_sequence_pre_init_flag_force_config"></a>NFC\_CX\_系列\_预\_INIT\_标志\_强制\_配置

0x00000002

此标志用于在 NCI 初始化之后强制执行更新配置。 通常情况下，如果控制器不支持保留配置，或在更新驱动程序之后配置已更改，则 NFC CX 仅更新配置。 驱动程序使用会话 ID 保存当前配置。

### <a name="nfc_cx_sequence_init_complete_flag_redo"></a>NFC\_CX\_序列\_INIT\_完成\_标志\_重做

0x00000001

此标志在 init complete 序列中用于重做初始化顺序。 如果客户端驱动程序已执行需要重新启动的固件下载或更新的硬件设置，则通常使用此设置。

### <a name="nfc_cx_sequence_pre_nfcee_disc_flag_skip"></a>NFC\_CX\_系列\_\_NFCEE\_

0x00000001

此标志在 NFCEE 预发现序列过程中用于跳过执行 NFCEE discovery。

### <a name="nfc_cx_sequence_pre_shutdown_flag_skip_reset"></a>NFC\_CX\_序列\_\_关闭\_标志\_跳过\_重置

0x00000001

此标志强制 NFC CX 在关闭期间不发送 NCI 重置。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC 类扩展（CX）参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

