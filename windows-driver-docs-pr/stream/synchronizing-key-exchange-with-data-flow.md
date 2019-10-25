---
title: 将密钥交换与数据流同步
description: 将密钥交换与数据流同步
ms.assetid: 54abc258-d26a-4d42-a5aa-712cdae76b6d
keywords:
- DVD 解码器微型驱动程序 WDK，版权保护
- 解码器微型驱动程序 WDK DVD，版权保护
- 版权保护 WDK DVD 解码器
- 密钥交换 WDK DVD 解码器
- 解密 WDK DVD 解码器
- 加密 WDK DVD 解码器
- 加密 WDK DVD 解码器
- DVD decrypters WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f4ff0c369f0512976a4c980fe29977a0676b17c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843590"
---
# <a name="synchronizing-key-exchange-with-data-flow"></a>将密钥交换与数据流同步





在处理上一个密钥中的所有数据之前，密钥交换过程可能会开始。 这种情况的一个示例是：从尾部标题过渡到在某些电影上设置的主程序标题中。 每个数据包的[**KSSTREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)结构的**TypeSpecificFlags**成员中存在一个标志。 此标志为**KS\_AM\_UseNewCSSKey**，这是在*ksmedia*中定义的。 它表示紧接在标头之后的数据示例就是新标题键适用的第一个数据示例。

如果 decrypter 在仍使用旧密钥的情况下可以处理新的密钥交换，则在接收属性时，DVD 解码器微型驱动程序应处理密钥交换。 如果 decrypter 必须等待，直到处理完需要上一个密钥的所有电影数据后，decrypter 将保留**Set**属性的 SRB。 Decrypter 使用[**ks\_DVDCOPY\_集\_COPY\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_set_copy_state)结构与参数**KS\_DVDCOPYSTATE\_initialize** or **ks\_DVDCOPYSTATE\_初始化\_标题**，直到接收到连接到它的所有流上的**KS\_AM\_UseNewCSSKey**标志。 之后，在该点之前，DVD 解码器微型驱动程序将处理收到的所有数据包。 这可以防止对数据使用不正确的键。

 

 




