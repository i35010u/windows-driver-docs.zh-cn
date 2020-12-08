---
title: 智能卡设计指南
description: 智能卡设计指南
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af8dbb2ebccb592525e45438ec4b7ca22c658641
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813603"
---
# <a name="smart-card-design-guide"></a>智能卡设计指南


通过智能卡 DDI，呼叫者可以通过 NFC 设备驱动程序在 NFC contactless 智能卡上执行低级别的智能卡操作。 这包括侦听卡到达/出发通知、读取智能卡的元数据（如 ATR、UID 和历史字节信息），以及使用 Apdu 对特定 NFC 卡执行读/写操作。 对于非 ISO14443 兼容的卡 (称为存储卡) ，存储卡支持的 Apdu 转换为低级基元命令，如4.3.7 中所述。 IOCTLs 构成智能卡设备驱动程序接口，所有这些接口都使用文件的 \_ 任何 \_ 访问和方法进行 \_ 缓冲处理。 下面的智能卡 DDI 是 Windows 1 指定的智能卡驱动程序 IOCTLs 的最小 \[ 子集 \] ，用于支持访问 NFC contactless 智能卡。

``` syntax
GUID_DEVINTERFACE_SMARTCARD_READER
“{50DD5230-BA8A-11D1-BF5D-0000F805F530}”
```

## <a name="unsupported-ioctls"></a>不支持的 IOCTLs


以下 IOCTLs 不支持 NFC 智能卡操作，因为它们不适用于 contactless 智能卡操作，因此驱动程序可能会返回不受支持的错误代码：

-   IOCTL \_ 智能卡 \_ 弹出
-   IOCTL \_ 智能卡 \_ 获取 \_ 上一个 \_ 错误
-   IOCTL \_ 智能卡 \_ 吞并

## <a name="smart-card-attributes"></a>智能卡属性
Windows 智能卡 DDI 包含 Get 和 Set 属性的 IOCTL 请求。 为了满足支持 NFC contactless reader 的最低要求，我们仅支持最小读取器和 ICC 状态集的 GET_ATTRIBUTE。 有关详细信息，请参阅 [支持的智能卡属性](smart-card-attributes.md)。

## <a name="in-this-section"></a>在本节中


-   [功能流](functional-flow.md)
-   [示例序列](example-sequence.md)
-   [存储卡要求](storage-card-requirements.md)
-   [支持的智能卡属性](smart-card-attributes.md)
-   [PC/SC 接口](pc-sc-interface.md)
 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[智能卡 DDI 和命令参考](/previous-versions/dn905601(v=vs.85))
