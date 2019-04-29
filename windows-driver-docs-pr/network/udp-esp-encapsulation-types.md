---
title: UDP-ESP 封装类型
description: UDP-ESP 封装类型
ms.assetid: 126d2fd5-778e-43ff-87f6-5b0b54a83bac
keywords:
- UDP 封装的 ESP 数据包 WDK IPsec 卸载、 封装类型和子
- 封装 WDK UDP ESP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1dc8ff441c908c7b1e9a395ace740e5601dfed6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358358"
---
# <a name="udp-esp-encapsulation-types"></a>UDP-ESP 封装类型

\[IPsec 任务卸载功能已弃用，不应使用。\]




下图显示了 Internet 密钥交换 (IKE) 数据包和 ESP 受保护的数据端口 4500 收到的数据包的 UDP 封装。

![说明端口 4500 的基本 udp esp 封装的关系图](images/4500-encap-types.png)

请注意按照 IKE 数据包中的 UDP 标头的零四个字节。 此字段的零用于 IKE 数据包与端口 4500 上的 UDP 封装 ESP 数据包区分开来。 而不是零，ESP 标头的数据包中的此位置具有非零的 ESP 标头。

### <a name="udp-esp-encapsulation-subtypes"></a>UDP ESP 封装子类型

ESP 数据包端口 4500 上的可根据下列 UDP ESP 封装子类型之一进行格式设置：

-   UDP 封装的传输。

    ESP 封装的传输模式数据包通过 UDP 封装。

-   UDP 封装隧道。

    数据包隧道模式部分是 UDP 封装。 数据包的传输模式部分不是 UDP 封装，并且未被 ESP 保护。

-   通过 UDP 封装隧道传输。

    数据包隧道模式部分是 UDP 封装。 数据包的传输模式部分不 UDP 封装，而是 ESP 保护。

-   UDP 封装通过隧道传输。

    数据包隧道模式部分不是 UDP 封装。 数据包的传输模式部分是 UDP 封装和 ESP 保护。

请注意，通过 UDP 封装隧道的 UDP 封装传输不受支持的封装子类型。

下图显示了端口 4500 UDP ESP 封装子类型。

![说明端口 4500 udp esp 封装子类型的关系图](images/4500-encap-subtypes.png)

 

 





