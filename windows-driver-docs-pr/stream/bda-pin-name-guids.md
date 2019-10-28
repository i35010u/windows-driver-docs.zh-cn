---
title: BDA 引脚名称 GUID
description: BDA 引脚名称 GUID
ms.assetid: 098e4c49-13dd-4c9a-8ce4-06b99b7c5fa3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3b7c68f3af51eb0cd9d356311f15ebd44379f46
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840615"
---
# <a name="bda-pin-name-guids"></a>BDA 引脚名称 GUID


## <span id="ddk_bda_pin_name_guids_ks"></span><span id="DDK_BDA_PIN_NAME_GUIDS_KS"></span>


BDA 微型驱动程序使用 BDA pin 名称 Guid 指定其支持的 pin 的名称和类别。 BDA 微型驱动程序将这些 Guid 分配给[**KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)结构的**名称**和**类别**成员。 *Bdamedia*头文件定义这些 guid。 筛选器的 pin 指定其名称和类别以连接到其他筛选器的 pin，这些其他筛选器也指定这些名称和类别。

以下 pin 名称 Guid 可用于 BDA：

<span id="PINNAME_BDA_TRANSPORT"></span><span id="pinname_bda_transport"></span>PINNAME\_BDA\_传输  
端口的端口名称。

<span id="PINNAME_BDA_ANALOG_VIDEO"></span><span id="pinname_bda_analog_video"></span>PINNAME\_BDA\_模拟\_视频  
BDA 模拟视频 pin 的 pin 名称。

<span id="PINNAME_BDA_ANALOG_AUDIO"></span><span id="pinname_bda_analog_audio"></span>PINNAME\_BDA\_模拟\_音频  
BDA 模拟音频 pin 的 Pin 名称。

<span id="PINNAME_BDA_FM_RADIO"></span><span id="pinname_bda_fm_radio"></span>PINNAME\_BDA\_FM\_无线电  
端口的端口名称。

<span id="PINNAME_BDA_IF_PIN"></span><span id="pinname_bda_if_pin"></span>如果\_PIN，则 PINNAME\_BDA\_  
BDA 中间频率 pin 的 Pin 名称。

<span id="PINNAME_BDA_OPENCABLE_PSIP_PIN"></span><span id="pinname_bda_opencable_psip_pin"></span>PINNAME\_BDA\_OPENCABLE\_PSIP\_PIN  
用于打开 BDA 电缆 PSIP 的 pin 的名称。

<span id="PINNAME_IPSINK_INPUT"></span><span id="pinname_ipsink_input"></span>PINNAME\_IPSINK\_输入  
输入插针到 BDA IP 接收器节点的名称（KSNODE\_BDA\_IP\_接收器）。

<span id="PINNAME_MPE"></span><span id="pinname_mpe"></span>PINNAME\_MPE  
多协议封装（MPE） pin 的 pin 名称。

 

 





