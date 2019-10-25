---
title: 智能卡设计指南
description: 智能卡设计指南
ms.assetid: 721A1530-B7B4-4373-9006-356A0A601349
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f3389aab004b28e499febf2114ad65942ead5b0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843428"
---
# <a name="smart-card-design-guide"></a>智能卡设计指南


通过智能卡 DDI，呼叫者可以通过 NFC 设备驱动程序在 NFC contactless 智能卡上执行低级别的智能卡操作。 这包括侦听卡到达/出发通知、读取智能卡的元数据（如 ATR、UID 和历史字节信息），以及使用 Apdu 对特定 NFC 卡执行读/写操作。 对于不符合 ISO14443 标准的卡（称为存储卡），在4.3.7 节中记录 Apdu 到存储卡支持的低级别基元命令的转换。 IOCTLs 构成了智能卡设备驱动程序接口，它们都使用文件\_任何\_访问和\_缓冲的方法。 下面的智能卡 DDI 是 Windows \[1\] 指定的智能卡驱动程序 IOCTLs 的最小子集，用于支持访问 NFC contactless 智能卡。

``` syntax
GUID_DEVINTERFACE_SMARTCARD_READER
“{50DD5230-BA8A-11D1-BF5D-0000F805F530}”
```

## <a name="unsupported-ioctls"></a>不支持的 IOCTLs


以下 IOCTLs 不支持 NFC 智能卡操作，因为它们不适用于 contactless 智能卡操作，因此驱动程序可能会返回不受支持的错误代码：

-   IOCTL\_智能卡\_弹出
-   IOCTL\_智能卡\_获取\_最后\_错误
-   IOCTL\_智能卡\_吞并

## <a name="smart-card-attributes"></a>智能卡属性
Windows 智能卡 DDI 包含 Get 和 Set 属性的 IOCTL 请求。 为了满足支持 NFC contactless reader 的最低要求，我们仅支持最小的一组读取器和 ICC 状态的 GET_ATTRIBUTE。 有关详细信息，请参阅[支持的智能卡属性](smart-card-attributes.md)。

## <a name="in-this-section"></a>本部分内容


-   [功能流](functional-flow.md)
-   [序列示例](example-sequence.md)
-   [存储卡要求](storage-card-requirements.md)
-   [支持的智能卡属性](smart-card-attributes.md)
-   [PC/SC 接口](pc-sc-interface.md)
 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[智能卡 DDI 和命令参考](https://docs.microsoft.com/previous-versions/dn905601(v=vs.85))  

