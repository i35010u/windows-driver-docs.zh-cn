---
title: GPIO 扩展
description: 常规用途输入/输出 (GPIO) 扩展命令显示 GPIO 控制器软件的状态。
ms.assetid: 1703C402-D770-4D3F-AB70-F2D30712A5D9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f35df5cb6bc7b76170002ba43a3a4cfcaae20795
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370863"
---
# <a name="gpio-extensions"></a>GPIO 扩展


常规用途输入/输出 (GPIO) 扩展命令显示 GPIO 控制器软件的状态。 这些命令将显示由 GPIO framework 扩展驱动程序 (Msgpioclx.sys) 维护的数据结构中的信息。 GPIO 框架扩展有关的信息，请参阅[常规用途 I/O (GPIO) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=299823)。

GPIO 调试器扩展命令 gpiokd.dll 中实现。 若要加载的 GPIO 命令，请输入 **.load gpiokd.dll**在调试器中。

每个 GPIO 控制器具有一系列银行。 组，每组具有包含数组的 pin 的 pin 表。 GPIO 调试器扩展命令显示有关 GPIO 控制器、 银行、 pin 表和 pin 信息。

## <a name="span-iddata-structures-used-by-the-gpio-commandsspanspan-iddatastructuresusedbythegpiocommandsspandata-structures-used-by-the-gpio-commands"></a><span id="data-structures-used-by-the-gpio-commands"></span><span id="DATA_STRUCTURES_USED_BY_THE_GPIO_COMMANDS"></span>GPIO 命令所使用的数据结构


GPIO 调试器扩展命令使用这些数据结构，由 Msgpioclx.sys 定义。

<span id="msgpioclx__DEVICE_EXTENSION"></span><span id="msgpioclx__device_extension"></span><span id="MSGPIOCLX__DEVICE_EXTENSION"></span>**msgpioclx!\_DEVICE\_EXTENSION**  
GPIO framework 扩展驱动程序设备扩展结构。 此结构保存有关单个的 GPIO 控制器的信息。

<span id="msgpioclx__GPIO_BANK_ENTRY"></span><span id="msgpioclx__gpio_bank_entry"></span><span id="MSGPIOCLX__GPIO_BANK_ENTRY"></span>**msgpioclx!\_GPIO\_BANK\_ENTRY**  
此结构保存有关单个银行 GPIO 控制器的信息。

<span id="msgpioclx__GPIO_PIN_INFORMATION_ENTRY"></span><span id="msgpioclx__gpio_pin_information_entry"></span><span id="MSGPIOCLX__GPIO_PIN_INFORMATION_ENTRY"></span>**msgpioclx ！\_GPIO\_PIN\_信息\_条目**  
此结构的银行 GPIO 控制器保存有关单个 pin 信息。

## <a name="span-idgettingstartedwithgpiodebuggingspanspan-idgettingstartedwithgpiodebuggingspanspan-idgettingstartedwithgpiodebuggingspangetting-started-with-gpio-debugging"></a><span id="Getting_started_with_GPIO_debugging"></span><span id="getting_started_with_gpio_debugging"></span><span id="GETTING_STARTED_WITH_GPIO_DEBUGGING"></span>开始使用 GPIO 调试


若要开始调试 GPIO 问题，请输入[ **！ gpiokd.clientlist** ](-gpiokd-clientlist.md)命令。 **！ Gpiokd.clientlist**命令显示所有已注册的 GPIO 控制器和显示地址，可以将它们传递给其他 GPIO 调试器命令的概述。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><a href="-gpiokd-help.md" data-raw-source="[!gpiokd.help](-gpiokd-help.md)">!gpiokd.help</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-help.md" data-raw-source="[!gpiokd.help](-gpiokd-help.md)">！ Gpiokd.help</a></strong>命令显示 GPIO 调试器扩展命令的帮助。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-gpiokd-bankinfo.md" data-raw-source="[!gpiokd.bankinfo](-gpiokd-bankinfo.md)">!gpiokd.bankinfo</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-bankinfo.md" data-raw-source="[!gpiokd.bankinfo](-gpiokd-bankinfo.md)">！ Gpiokd.bankinfo</a></strong>命令显示有关 GPIO 银行信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-gpiokd-clientlist.md" data-raw-source="[!gpiokd.clientlist](-gpiokd-clientlist.md)">!gpiokd.clientlist</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-clientlist.md" data-raw-source="[!gpiokd.clientlist](-gpiokd-clientlist.md)">！ Gpiokd.clientlist</a></strong>命令显示所有已注册的 GPIO 控制器。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-gpiokd-gpioext.md" data-raw-source="[!gpiokd.gpioext](-gpiokd-gpioext.md)">!gpiokd.gpioext</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-gpioext.md" data-raw-source="[!gpiokd.gpioext](-gpiokd-gpioext.md)">！ Gpiokd.gpioext</a></strong>命令显示有关 GPIO 控制器的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-gpiokd-pininfo.md" data-raw-source="[!gpiokd.pininfo](-gpiokd-pininfo.md)">!gpiokd.pininfo</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-pininfo.md" data-raw-source="[!gpiokd.pininfo](-gpiokd-pininfo.md)">！ Gpiokd.pininfo</a></strong>命令显示有关指定的 GPIO pin 信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-gpiokd-pinisrvec.md" data-raw-source="[!gpiokd.pinisrvec](-gpiokd-pinisrvec.md)">!gpiokd.pinisrvec</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-pinisrvec.md" data-raw-source="[!gpiokd.pinisrvec](-gpiokd-pinisrvec.md)">！ Gpiokd.pinisrvec</a></strong>命令显示指定的 pin 的中断服务例程 (ISR) 向量信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-gpiokd-pintable.md" data-raw-source="[!gpiokd.pintable](-gpiokd-pintable.md)">!gpiokd.pintable</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-pintable.md" data-raw-source="[!gpiokd.pintable](-gpiokd-pintable.md)">！ Gpiokd.pintable</a></strong>命令显示有关数组的 GPIO 插针的信息。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[专用的扩展命令](specialized-extensions.md)

 

 






