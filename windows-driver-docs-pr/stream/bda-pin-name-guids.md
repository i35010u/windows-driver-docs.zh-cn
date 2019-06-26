---
title: BDA 引脚名称 GUID
description: BDA 引脚名称 GUID
ms.assetid: 098e4c49-13dd-4c9a-8ce4-06b99b7c5fa3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2287965222b0636cd298ed2e0dd3549084441fed
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386683"
---
# <a name="bda-pin-name-guids"></a>BDA 引脚名称 GUID


## <span id="ddk_bda_pin_name_guids_ks"></span><span id="DDK_BDA_PIN_NAME_GUIDS_KS"></span>


BDA 微型驱动程序使用 BDA pin 名称 Guid 来指定名称和类别的 pin，它支持。 BDA 微型驱动程序将这些分配到 Guid**名称**并**类别**的成员[ **KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_descriptor)结构。 *Bdamedia.h*标头文件定义了这些 Guid。 筛选器的插针指定其名称和类别来连接到这些名称和类别还指定其他筛选器的 pin。

BDA 中提供了以下固定名称 Guid:

<span id="PINNAME_BDA_TRANSPORT"></span><span id="pinname_bda_transport"></span>PINNAME\_BDA\_传输  
BDA 传输 pin 的固定名称。

<span id="PINNAME_BDA_ANALOG_VIDEO"></span><span id="pinname_bda_analog_video"></span>PINNAME\_BDA\_模拟\_视频  
对于 BDA 模拟视频插针的固定名称。

<span id="PINNAME_BDA_ANALOG_AUDIO"></span><span id="pinname_bda_analog_audio"></span>PINNAME\_BDA\_模拟\_音频  
BDA 模拟音频插针的固定名称。

<span id="PINNAME_BDA_FM_RADIO"></span><span id="pinname_bda_fm_radio"></span>PINNAME\_BDA\_FM\_RADIO  
BDA FM 单选 pin 的固定名称。

<span id="PINNAME_BDA_IF_PIN"></span><span id="pinname_bda_if_pin"></span>PINNAME\_BDA\_如果\_PIN  
BDA 中间频率 pin 的固定名称。

<span id="PINNAME_BDA_OPENCABLE_PSIP_PIN"></span><span id="pinname_bda_opencable_psip_pin"></span>PINNAME\_BDA\_OPENCABLE\_PSIP\_PIN  
BDA 打开电缆 PSIP pin 的固定名称。

<span id="PINNAME_IPSINK_INPUT"></span><span id="pinname_ipsink_input"></span>PINNAME\_IPSINK\_INPUT  
Pin 输入插针到 BDA IP 汇聚节点的名称 (KSNODE\_BDA\_IP\_接收器)。

<span id="PINNAME_MPE"></span><span id="pinname_mpe"></span>PINNAME\_MPE  
多协议封装 (MPE) pin 的固定名称。

 

 





