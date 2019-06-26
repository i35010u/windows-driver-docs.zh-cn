---
title: Windows 设备测试框架 (WDTF) 设计指南
description: 使用 Microsoft Windows 设备测试框架 (WDTF)，你可以创建、管理、重用和扩展以设备为中心、基于方案的自动化测试。
ms.assetid: cff552f0-5dde-4fe7-996c-0a496d845edc
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 384c94766125e06cbdac0d70bdb940b00cb01b0d
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393472"
---
# <a name="windows-device-testing-framework-wdtf-design-guide"></a>Windows 设备测试框架 (WDTF) 设计指南


使用 Microsoft Windows 设备测试框架 (WDTF)，你可以创建、管理、重用和扩展以设备为中心、基于方案的自动化测试。

## <a name="in-this-section"></a>本部分内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="writing-a-wdtf-simpleio-plug-in-for-your-device.md" data-raw-source="[Writing a WDTF SimpleIO plug-in for your device](writing-a-wdtf-simpleio-plug-in-for-your-device.md)">为你的设备编写 WDTF SimpleIO 插件</a></p></td>
<td><p>若要充分利用<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamental tests](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试</a>，你的设备应当有一个可以对设备执行简单 I/O 操作的简单 I/O 插件。 这可以是 WDTF 附带的默认简单 I/O 插件之一，也可以是你自己编写的插件。 若要了解设备类型是否受支持以及确定是否有特定的测试要求，请参阅<a href="provided-wdtf-simpleio-plug-ins.md" data-raw-source="[Provided WDTF Simple I/O plug-ins](provided-wdtf-simpleio-plug-ins.md)">提供的 WDTF 简单 I/O 插件</a>。</p></td>
</tr>
<tr class="even">
<td><p><a href="writing-tests-with-wdtf.md" data-raw-source="[Writing tests with WDTF](writing-tests-with-wdtf.md)">使用 WDTF 编写测试</a></p></td>
<td><p>无论你是使用 Windows 驱动程序工具包 (WDK) 中提供的模板开始编写驱动程序测试，还是自己创建测试，你都可以借助 Microsoft Windows 设备测试框架 (WDTF) 来创建和扩展以设备为中心、基于方案的自动化测试。</p></td>
</tr>
<tr class="odd">
<td><p><a href="triaging-wdtf-based-tests.md" data-raw-source="[Triaging WDTF-based tests](triaging-wdtf-based-tests.md)">会审基于 WDTF 的测试</a></p></td>
<td><p>为了帮助你更好地理解基于 WDTF 的测试中发生的情况，你可以使用内置的 <a href="logging-and-tracing.md" data-raw-source="[WDTF Object Logging](logging-and-tracing.md)">WDTF 对象日志记录</a>和 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing" data-raw-source="[WPP Software Tracing](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)">WPP 软件跟踪</a>支持。</p></td>
</tr>
<tr class="even">
<td><p><a href="wdtf-overview.md" data-raw-source="[WDTF Architecture and Overview](wdtf-overview.md)">WDTF 体系结构和概述</a></p></td>
<td><p>使用 Microsoft Windows 设备测试框架 (WDTF)，你可以创建、管理、重用和扩展以设备为中心、基于方案的自动化测试。</p></td>
</tr>
</tbody>
</table>

 

 

 




