---
title: 序列标志
description: NFC CX 为序列事件定义以下常量。
keywords:
- NFC
- 近场通信
- 近程
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
ms.openlocfilehash: 9b87eae993ce3347aaf49a21ceef82bcef7bd50c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812729"
---
# <a name="sequence-flags"></a>序列标志


NFC CX 为序列事件定义以下常量。


### <a name="nfc_cx_sequence_pre_init_flag_skip_config"></a>NFC \_ CX \_ 序列 \_ 预先 \_ 初始 \_ 标志 \_ 跳过 \_ 配置

0x00000001

此标志在预初始化序列中用于在 NCI 初始化后跳过配置更新。 请注意，此标志不能与 force 配置选项一起使用。

### <a name="nfc_cx_sequence_pre_init_flag_force_config"></a>NFC \_ CX \_ 序列 \_ 预先 \_ 初始 \_ 标志 \_ 强制 \_ 配置

0x00000002

此标志用于在 NCI 初始化之后强制执行更新配置。 通常情况下，如果控制器不支持保留配置，或在更新驱动程序之后配置已更改，则 NFC CX 仅更新配置。 驱动程序使用会话 ID 保存当前配置。

### <a name="nfc_cx_sequence_init_complete_flag_redo"></a>NFC \_ CX \_ 序列 \_ 初始化 \_ 完成 \_ 标志 \_ 重做

0x00000001

此标志在 init complete 序列中用于重做初始化顺序。 如果客户端驱动程序已执行需要重新启动的固件下载或更新的硬件设置，则通常使用此设置。

### <a name="nfc_cx_sequence_pre_nfcee_disc_flag_skip"></a>NFC \_ CX \_ 序列 \_ PRE \_ NFCEE \_ 光盘 \_ 标志 \_ 跳过

0x00000001

此标志在 NFCEE 预发现序列过程中用于跳过执行 NFCEE discovery。

### <a name="nfc_cx_sequence_pre_shutdown_flag_skip_reset"></a>NFC \_ CX \_ 序列 \_ 预 \_ 关闭 \_ 标志 \_ 跳过 \_ 重置

0x00000001

此标志强制 NFC CX 在关闭期间不发送 NCI 重置。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[ (CX) 参考的 NFC 类扩展](/windows-hardware/drivers/ddi/index)
