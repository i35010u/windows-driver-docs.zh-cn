---
title: 序列标志
description: NFC CX 定义以下常量的序列事件。
ms.assetid: AC6CE286-52F7-4FC9-9F38-CD10C1413A90
keywords:
- NFC
- 附近通信
- 近程
- 邻近附近
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
ms.openlocfilehash: 71441dadf2bb8922d6e2f1f0a1ec0b25f4c520f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554134"
---
# <a name="sequence-flags"></a>序列标志


NFC CX 定义以下常量的序列事件。


### <a name="nfccxsequencepreinitflagskipconfig"></a>NFC\_CX\_序列\_PRE\_INIT\_标志\_跳过\_配置

0x00000001

此标志初始化前序列中用于跳过 NCI 初始化后的配置更新。 请注意此标志不能与 force 配置选项一起使用。

### <a name="nfccxsequencepreinitflagforceconfig"></a>NFC\_CX\_SEQUENCE\_PRE\_INIT\_FLAG\_FORCE\_CONFIG

0x00000002

此标志用于强制 NCI 初始化之后更新配置。 通常情况下，NFC CX 仅更新配置如果控制器不支持保留配置或如果驱动程序更新后的配置已更改。 该驱动程序仍然存在当前配置使用会话 id。

### <a name="nfccxsequenceinitcompleteflagredo"></a>NFC\_CX\_SEQUENCE\_INIT\_COMPLETE\_FLAG\_REDO

0x00000001

Init 完整序列中使用此标志重新初始化序列。 这通常使用客户端驱动程序已执行固件下载或更新需要重新启动的硬件设置。

### <a name="nfccxsequenceprenfceediscflagskip"></a>NFC\_CX\_SEQUENCE\_PRE\_NFCEE\_DISC\_FLAG\_SKIP

0x00000001

此标志用于 NFCEE 预发现序列期间跳过执行 NFCEE 发现。

### <a name="nfccxsequencepreshutdownflagskipreset"></a>NFC\_CX\_SEQUENCE\_PRE\_SHUTDOWN\_FLAG\_SKIP\_RESET

0x00000001

此标志强制 NFC CX 不发送 NCI 在关闭期间重置。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC 类扩展 (CX) 引用](https://msdn.microsoft.com/library/windows/hardware/dn905536)  

