---
title: 智能卡设计指南
description: 智能卡设计指南
ms.assetid: 721A1530-B7B4-4373-9006-356A0A601349
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 202a3cf25f39e6a3cd15059f212c1e7e9d3c674d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370544"
---
# <a name="smart-card-design-guide"></a>智能卡设计指南


智能卡 DDI 允许 NFC 的设备驱动程序调用方执行 NFC 非接触式智能卡上的低级别的智能卡操作。 这包括侦听卡到达/出发通知，读取智能卡 ATR、 UID 和历史字节信息之类的元数据，以及执行使用 Apdu 特定 NFC 卡上的读/写操作。 对于非 ISO14443 4 符合卡 （称为存储卡），到支持的存储卡的低级别基元命令的 Apdu 翻译一节介绍了 4.3.7。 Ioctl 组成的智能卡设备驱动程序接口，所有这些使用文件\_ANY\_访问和方法\_缓冲。 智能卡 DDI 下面是智能卡驱动程序指定的 Windows Ioctl 最小子集\[1\]以支持访问 NFC 非接触式智能卡。

``` syntax
GUID_DEVINTERFACE_SMARTCARD_READER
“{50DD5230-BA8A-11D1-BF5D-0000F805F530}”
```

## <a name="unsupported-ioctls"></a>不支持的 Ioctl


NFC 智能卡操作不支持以下 Ioctl 是因为它们不是适用于非接触式智能卡操作，因此驱动程序可能会返回不受支持的错误代码：

-   IOCTL\_智能卡\_弹出
-   IOCTL\_智能卡\_获取\_最后一个\_错误
-   IOCTL\_智能卡\_抑制

## <a name="smart-card-attributes"></a>智能卡属性
Windows 智能卡 DDI 包括 IOCTL 请求的 Get 和 Set 属性。 为了满足支持 NFC 非接触式读取器的最低要求，我们仅支持 GET_ATTRIBUTE 用于读取器和 ICC 状态的最小集。 有关详细信息，请参阅[支持的智能卡属性](smart-card-attributes.md)。

## <a name="in-this-section"></a>本节内容


-   [功能的流](functional-flow.md)
-   [序列示例](example-sequence.md)
-   [存储卡的要求](storage-card-requirements.md)
-   [支持的智能卡属性](smart-card-attributes.md)
-   [PC/SC 接口](pc-sc-interface.md)
 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[智能卡 DDI 和命令参考](https://docs.microsoft.com/previous-versions/dn905601(v=vs.85))  

