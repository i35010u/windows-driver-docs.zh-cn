---
title: 将密钥交换与数据流同步
description: 将密钥交换与数据流同步
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
ms.openlocfilehash: 4a4112be94f1eec45c7d239b911b817a921b7b2a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840489"
---
# <a name="synchronizing-key-exchange-with-data-flow"></a>将密钥交换与数据流同步





在处理上一个密钥中的所有数据之前，密钥交换过程可能会开始。 这种情况的一个示例是：从尾部标题过渡到在某些电影上设置的主程序标题中。 每个数据包的 [**KSSTREAM \_ 标头**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)结构的 **TypeSpecificFlags** 成员中都有一个标志。 此标志为 **KS \_ AM \_ UseNewCSSKey**，它是在 *ksmedia* 中定义的。 它表示紧接在标头之后的数据示例就是新标题键适用的第一个数据示例。

如果 decrypter 在仍使用旧密钥的情况下可以处理新的密钥交换，则在接收属性时，DVD 解码器微型驱动程序应处理密钥交换。 如果 decrypter 必须等待，直到处理完需要上一个密钥的所有电影数据后，decrypter 将保留 **Set** 属性的 SRB。 Decrypter 对参数 **ks \_ DVDCOPYSTATE \_ initialize** 或 **KS \_ DVDCOPYSTATE \_ initialize \_ TITLE** 使用 [**ks \_ DVDCOPY \_ 集 \_ 复制 \_ 状态**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_set_copy_state)结构，直到它在连接到它的所有流上收到 **KS \_ AM \_ UseNewCSSKey** 标志。 之后，在该点之前，DVD 解码器微型驱动程序将处理收到的所有数据包。 这可以防止对数据使用不正确的键。

 

