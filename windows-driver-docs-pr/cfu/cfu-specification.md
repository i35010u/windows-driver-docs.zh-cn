---
title: 组件固件更新 (CFU) 协议规范
description: 提供有关组件固件更新 (CFU) 协议提议、内容和固件更新命令序列的详细信息。
ms.date: 10/01/2020
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: 51852681f48127e1c75adbba8419d2f54889b3be
ms.sourcegitcommit: eefc6ae6d9621d0735b3c63e718ee5838d57a6bc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92886352"
---
# <a name="component-firmware-update-cfu-protocol-specification"></a>组件固件更新 (CFU) 协议规范

此规范描述了用于更新 PC 或附件上存在的组件固件的一般 HID 协议。 此规范允许组件接受固件，而不会在下载期间中断设备操作。 该规范支持配置，其中接受固件的组件可能包含需要单独固件映像的子组件。 该规范允许组件进行计费以决定是否接受固件。 它还可用作优化，因为固件映像只会发送到组件，如果它能够或准备接受它。

## <a name="contents"></a>目录

- [1简介](#1-introduction)
  - [1.1 术语表](#11-glossary)
  - [1.2 范围](#12-scope)
    - [1.2.1 目标](#121-goals)
    - [1.2.2 非目标](#122-non-goals)
- [2支持的硬件体系结构](#2-supported-hardware-architecture)
- [3协议先决条件](#3-protocol-prerequisites)
- [4 CFU 协议概述](#4-cfu-protocol-overview)
  - [4.1 固件更新编程命令序列](#41-firmware-update-programming-command-sequence)
    - [4.1.1 状态：主机初始化通知](#411-state-host-initialized-notification)
    - [4.1.2 状态： OFFER_INFO_START_OFFER_LIST 通知](#412-state-offer_info_start_offer_list-notification)
    - [4.1.3 状态： Send FIRMWARE_UPDATE_OFFER 命令](#413-state-send-firmware_update_offer-command)
    - [4.1.4 状态：发送固件](#414-state-send-firmware)
    - [4.1.5 决策状态：是否有更多优惠](#415-decision-state-are-there-more-offers)
    - [4.1.6 状态： OFFER_INFO_END_OFFER_LIST 通知](#416-state-offer_info_end_offer_list-notification)
    - [4.1.7 决策状态：重播提议列表](#417-decision-state-replay-offer-list)
    - [4.1.8 状态：设备繁忙](#418-state-device-is-busy)
- [5 CFU 协议数据包格式](#5-cfu-protocol-packet-format)
  - [5.1 GET_FIRMWARE_VERSION](#51-get_firmware_version)
    - [5.1.1 命令](#511-command)
    - [5.1.2 响应](#512-response)
      - [5.1.2.1 标头](#5121-header)
      - [5.1.2.2 组件版本和属性](#5122-component-version-and-properties)
    - [5.1.3 映射到 HID](#513-mapping-to-hid)
  - [5.2 FIRMWARE_UPDATE_OFFER](#52-firmware_update_offer)
    - [5.2.1 命令](#521-command)
      - [5.2.1.1 组件信息](#5211-component-information)
      - [5.2.1.2 固件版本](#5212-firmware-version)
      - [5.2.1.3 供应商特定](#5213-vendor-specific)
      - [5.2.1.4 杂项协议版本](#5214-misc-and-protocol-version)
    - [5.2.2 响应](#522-response)
      - [5.2.2.1 标记](#5221-token)
      - [5.2.2.2 保留 (B7-B4) ](#5222-reserved-b7---b4)
      - [5.2.2.3 拒绝原因 (RR) ](#5223-reject-reason-rr)
      - [5.2.2.4 状态](#5224-status)
    - [5.2.3 映射到 HID 协议](#523-mapping-to-hid-protocol)
  - [5.3 FIRMWARE_UPDATE_OFFER-信息](#53-firmware_update_offer---information)
    - [5.3.1 命令](#531-command)
      - [5.3.1.1 组件](#5311-component)
      - [5.3.1.2 保留 B7-B4](#5312-reserved-b7---b4)
      - [5.3.1.3 Reserved B11-B8](#5313-reserved-b11---b8)
      - [5.3.1.4 Reserved B15-B12](#5314-reserved-b15---b12)
    - [5.3.2 响应](#532-response)
      - [5.3.2.1 标记](#5321-token)
      - [5.3.2.2 保留 B7-B4](#5322-reserved-b7---b4)
      - [5.3.2.3 拒绝原因 (RR) ](#5323-reject-reason-rr)
      - [5.3.2.4 状态](#5324-status)
  - [5.4 FIRMWARE_UPDATE_OFFER 扩展](#54-firmware_update_offer---extended)
    - [5.4.1 命令](#541-command)
      - [5.4.1.1 组件](#5411-component)
      - [5.4.1.2 保留 B7-B4](#5412-reserved-b7---b4)
      - [5.4.1.3 Reserved B11-B8](#5413-reserved-b11---b8)
      - [5.4.1.4 Reserved B15-B12](#5414-reserved-b15---b12)
    - [5.4.2 响应](#542-response)
      - [5.4.2.1 标记](#5421-token)
      - [5.4.2.2 保留 B7-B4](#5422-reserved-b7---b4)
      - [5.4.2.3 拒绝原因](#5423-reject-reason)
      - [5.4.2.4 状态](#5424-status)
  - [5.5 FIRMWARE_UPDATE_CONTENT](#55-firmware_update_content)
    - [5.5.1 命令](#551-command)
      - [5.5.1.1 标头 (B7-B0) ](#5511-header-b7---b0)
      - [5.5.1.2 数据](#5512-data)
    - [5.5.2 响应](#552-response)
      - [5.5.2.1 序列号](#5521-sequence-number)
      - [5.5.2.2 状态](#5522-status)
      - [5.5.2.3 Reserved B8-B11](#5523-reserved-b8---b11)
      - [5.5.2.4 Reserved B12-B15](#5524-reserved-b12---b15)
- [6附录1：固件更新编程命令序列示例](#6-appendix-1-example-firmware-update-programming-command-sequence)
  - [6.1 示例1](#61-example-1)
  - [6.2 示例2](#62-example-2)

## <a name="tables"></a>表

[表 5.1-1 GET_FIRMWARE_VERSION 响应布局](#table-51-1-get_firmware_version-response-layout)

[表 5.1-2 GET_FIRMWARE_VERSION 响应头布局](#table-51-2-get_firmware_version-response----header-layout)

[表 5.1-3 GET_FIRMWARE_VERSION 响应头位](#table-51-3-get_firmware_version-response---header-bits)

[表 5.1-4 GET_FIRMWARE_VERSION 响应-组件版本和属性布局](#table-51-4-get_firmware_version-response---component-version-and-properties-layout)

[表 5.1-5 GET_FIRMWARE_VERSION 响应-组件版本和属性片段](#table-51-5-get_firmware_version-response---component-version-and-properties-bites)

[表 5.2 FIRMWARE_UPDATE_OFFER 命令布局](#table-52-1-firmware_update_offer-command-layout)

[表 5.2-2 FIRMWARE_UPDATE_OFFER 命令-组件信息布局](#table-52-2-firmware_update_offer-command---component-information-layout)

[表 5.2 FIRMWARE_UPDATE_OFFER 命令-组件信息位](#table-52-3-firmware_update_offer-command---component-information-bits)

[表 5.2-4 FIRMWARE_UPDATE_OFFER 命令-固件版本布局](#table-52-4-firmware_update_offer-command---firmware-version-layout)

[表 5.2-5 FIRMWARE_UPDATE_OFFER 命令-固件版本位](#table-52-5-firmware_update_offer-command---firmware-version-bits)

[表 5.2-6 FIRMWARE_UPDATE_OFFER 命令特定于供应商的布局](#table-52-6-firmware_update_offer-command---vendor-specific-layout)

[表 5.2-7 FIRMWARE_UPDATE_OFFER 命令-其他和协议版本](#table-52-7-firmware_update_offer-command---misc-and-protocol-version)

[表 5.2-8 FIRMWARE_UPDATE_OFFER 响应令牌布局](#table-52-8-firmware_update_offer-response-token-layout)

[表 5.2-9 FIRMWARE_UPDATE_OFFER 响应-令牌布局](#table-52-9-firmware_update_offer-response---token-layout)

[表 5.2-10 FIRMWARE_UPDATE_OFFER 响应-令牌位](#table-52-10-firmware_update_offer-response---token-bits)

[表 5.2-11 FIRMWARE_UPDATE_OFFER 响应-拒绝原因布局](#table-52-11-firmware_update_offer-response---reject-reason-layout)

[表 5.2-12 固件 \_ 更新 \_ 提供响应-拒绝原因位](#table-52-12-firmware_update_offer-response---reject-reason-bits)

[表 5.2-13 固件 \_ 更新 \_ 提供响应 RR 代码值](#table-52-13-firmware_update_offer-response-rr-code-values)

[表 5.2-14 FIRMWARE_UPDATE_OFFER 响应状态布局](#table-52-14-firmware_update_offer-response-status-layout)

[表 5.2-15 FIRMWARE_UPDATE_OFFER 响应-状态位](#table-52-15-firmware_update_offer-response---status-bits)

[表 5.2-16 FIRMWARE_UPDATE_OFFER 响应状态值](#table-52-16-firmware_update_offer-response-status-values)

[表 5.3-1 FIRMWARE_UPDATE_OFFER-信息命令布局](#table-53-1-firmware_update_offer---information-command-layout)

[表 5.3-2 FIRMWARE_UPDATE_OFFER 信息命令-组件布局](#table-53-2-firmware_update_offer---information-command---component-layout)

[表 5.3-3 FIRMWARE_UPDATE_OFFER 信息命令-组件位](#table-53-3-firmware_update_offer---information-command---component-bits)

[表 5.3-4 FIRMWARE_UPDATE_OFFER 信息命令-信息代码值](#table-53-4-firmware_update_offer---information-command---information-code-values)

[表 5.3-5 FIRMWARE_UPDATE_OFFER-信息响应布局](#table-53-5-firmware_update_offer---information-response-layout)

[表 5.3-6 FIRMWARE_UPDATE_OFFER-信息数据包响应令牌布局](#table-53-6-firmware_update_offer--information-packet-response-token-layout)

[表 5.3-7 FIRMWARE_UPDATE_OFFER 信息响应-令牌位](#table-53-7-firmware_update_offer---information-response---token-bits)

[表 5.3-8 FIRMWARE_UPDATE_OFFER-信息响应-RR 代码布局](#table-53-8-firmware_update_offer---information-response---rr-code-layout)

[表 5.3-9 FIRMWARE_UPDATE_OFFER 提供信息响应-RR 代码位](#table-53-9-firmware_update_offer--offer-information-response---rr-code-bits)

[表 5.3-10 FIRMWARE_UPDATE_OFFER-信息响应-RR 代码值](#table-53-10-firmware_update_offer--information-response---rr-code-values)

[表 5.3-11 FIRMWARE_UPDATE_OFFER-产品/服务信息响应状态布局](#table-53-11-firmware_update_offer---offer-information-response-status-layout)

[表 5.3-12 FIRMWARE_UPDATE_OFFER-产品/服务信息-响应状态位](#table-53-12-firmware_update_offer---offer-information---response-status-bits)

[表 5.4 FIRMWARE_UPDATE_OFFER 扩展命令布局](#table-54-1-firmware_update_offer---extended-command-layout)

[表 5.4-2 FIRMWARE_UPDATE_OFFER 扩展命令数据包布局](#table-54-2-firmware_update_offer---extended-command-packet---command---component-layout)

[表 5.4 FIRMWARE_UPDATE_OFFER 扩展命令-组件位](#table-54-3-firmware_update_offer---extended-command---component-bits)

[表 5.4-4 FIRMWARE_UPDATE_OFFER 扩展命令-命令代码值](#table-54-4-firmware_update_offer---extended-command---command-code-values)

[表 5.4-5 FIRMWARE_UPDATE_OFFER 扩展命令数据包响应布局](#table-54-5-firmware_update_offer---extended-command-packet-response-layout)

[表 5.4-6 FIRMWARE_UPDATE_OFFER 提供命令数据包响应-令牌布局](#table-54-6-firmware_update_offer--offer-command-packet-response---token-layout)

[表 5.4-7 FIRMWARE_UPDATE_OFFER 提供命令响应-令牌位](#table-54-7-firmware_update_offer---offer-command-response---token-bits)

[表 5.4-8 FIRMWARE_UPDATE_OFFER 提供信息数据包响应 RR 布局](#table-54-8-firmware_update_offer---offer-information-packet-response-rr-layout)

[表 5.4-9 FIRMWARE_UPDATE_OFFER 提供命令响应-RR 代码](#table-54-9-firmware_update_offer--offer-command-response---rr-code)

[表 5.4 FIRMWARE_UPDATE_OFFER-提供命令数据包-RR Code 值](#table-54-10-firmware_update_offer--offer-command-packet---rr-code-values)

[表 5.4 FIRMWARE_UPDATE_OFFER-提供命令数据包响应状态布局](#table-54-11-firmware_update_offer---offer-command-packet-response-status-layout)

[表 5.4-12 FIRMWARE_UPDATE_OFFER 提供命令数据包响应 RR 代码](#table-54-12-firmware_update_offer--offer-command-packet-response-rr-code)

[表 5.5-1 FIRMWARE_UPDATE_CONTENT 命令布局](#table-55-1-firmware_update_content-command-layout)

[表 5.5-2 FIRMWARE_UPDATE_CONTENT 命令头布局](#table-55-2-firmware_update_content-command-header-layout)

[表 5.5-3 FIRMWARE_UPDATE_CONTENT 头位](#table-55-3-firmware_update_content-header-bits)

[表 5.5-4 FIRMWARE_UPDATE_OFFER 提供命令数据包标志值](#table-55-4-firmware_update_offer--offer-command-packet---flag-values)

[表 5.5-5 FIRMWARE_UPDATE_CONTENT 命令数据布局](#table-55-5-firmware_update_content-command-data-layout)

[表 5.5-6 FIRMWARE_UPDATE_CONTENT 命令数据位](#table-55-6-firmware_update_content-command-data-bits)

[表 5.5-7 FIRMWARE_UPDATE_CONTENT 命令响应布局](#table-55-7-firmware_update_content-command-response-layout)

[表 5.5-8 FIRMWARE_UPDATE_CONTENT 响应顺序号](#table-55-8-firmware_update_content-response---sequence-number)

[表 5.5-9 FIRMWARE_UPDATE_CONTENT 命令-响应位](#table-55-9-firmware_update_content---command---response-bits)

[表 5.5-10 FIRMWARE_UPDATE_CONTENT 响应状态布局](#table-55-10-firmware_update_content-response-status-layout)

[表 5.5-11 FIRMWARE_UPDATE_OFFER 响应-状态位](#table-55-11-firmware_update_offer---response---status-bits)

[表 5.5-12 FIRMWARE_UPDATE_OFFER 响应状态代码值](#table-55-12-firmware_update_offer--response---status-code-values)

## <a name="1-introduction"></a>1 简介

如今的 Pc 和附件具有执行复杂操作的内部组件。 若要确保质量的产品，需要经常更新这些设备的行为，以便在开发的更高阶段或将这些设备交付给客户之后。 更新可能会修复标识的功能或安全问题，或者需要添加新功能。 复杂逻辑的大部分是在设备上运行的固件中，这是可更新的。

此规范描述了用于更新计算机上存在的组件或其附件的固件的一般 HID 协议。 HID 实现超出规范的范围。

协议的一些功能包括：

- 协议基于 HID （无处不在），并且具有对各种互连总线（如 USB 和 I<sup>2</sup>C）的 Windows 内置支持。 因此，可以利用相同的软件 (驱动程序) 解决方案来更新所有组件的固件。

  > [!NOTE]
  > 由于规范是基于数据包的，因此将其调整为非 HID 方案非常简单。

- 此规范允许组件接受固件，而不会在下载过程中中断设备操作。 它为用户提供了更好的体验，因为用户无需等待固件更新过程完成即可继续执行其他任务。 在对用户影响最小的时间，可以在单个原子操作中调用新的固件。

- 该规范支持配置，其中接受固件的组件可能包含需要单独固件映像的子组件。

  > [!NOTE]
  > 组件通过固件向子组件进行处理的过程超出了本规范的范围。

- 该规范支持 *产品/服务* 的概念，并依赖于组件收费来决定是否接受固件。 接受新固件的决定并不简单。 固件类型和/或版本以及新固件适用的硬件的基础类型/版本之间可能存在依赖关系。 "产品/服务" 也充当一种优化机制，因为固件映像仅在能够/ready 接受它时才会发送到组件。

## <a name="11-glossary"></a>1.1 术语表

| 术语 | 说明 |
|--|--|
| 组件 ID | 在具有多个组件的设备中，组件 ID 唯一标识每个组件。 |
| CRC | 循环冗余检查<br><br>用于生成数据块的摘要或指纹的非加密哈希算法。 CRC 用作检查以确保数据块在计算 CRC 后未发生更改。 CRC 不可靠，但可以确信正确地接收了数据。 |
| 设备 | 组件的集合， (一个主组件以及零个或多个子组件) 。 设备在操作系统上作为一个单元显示。 主机与设备交互，该设备通常是主组件。<br><br>计算机上可能有多个设备。 对于此规范，与2个不同设备的通信完全是独立的。 |
| 驱动程序 | 使用 Windows Driver Foundation (WDF) framework 编写的驱动程序。 |
| 固件 | 在物理硬件上运行的代码。 固件可更新，并且通常位于与硬件关联的可编程内存中。 |
| 硬件 | 计算机上的一块芯片。 |
| 主要组件 | 计算机上的硬件和固件。 在此规范的上下文中，组件是需要和接受固件更新的实体。 |
| 段 | 组件的固件映像可能分为较小的段。 每个段都是小型固件映像。 |
| 段 ID | 如果将组件的固件分成较小的段，段 ID 就是段的唯一标识符。 |
| 签名 | 加密是指确定固件映像是否已由未经授权的方法更改。 签名是可选的，但建议并超出此规范的范围。 |
| 子组件 | 根据硬件体系结构，并非所有组件都可能对操作系统可见，因为它们可能连接到对系统可见的组件。 在此规范中，这些组件被称为子组件。 |
| TLC | HID 顶层集合。 |
| 令牌 | 主机会话的标识符。 主机会创建一个令牌并将其发送到命令，然后设备将在响应中返回该令牌。 标记可用于序列化某些事务或确定会话已丢失和另一次启动。 |

## <a name="12-scope"></a>1.2 范围

### <a name="121-goals"></a>1.2.1 目标

- 需要使用与总线无关的解决方案来避免为每种类型的总线提供新的协议。 HID 是通用的，并满足此要求。

- 支持多组件设备的固件更新的功能，其中一个组件充当主要组件，另一个组件作为连接到主组件的子组件。 每个组件都需要自己的固件，其中每个组件彼此之间不重要。

- 用于将固件映像下载到组件的通用驱动程序模型。 然后，该组件具有子组件特定的算法，用于转发到子组件。 子组件还可以对其固件执行有效性检查，并将结果传递回主组件。

- 设备操作正在进行时支持固件更新的能力。

- 能够通过授权工具在生产设备中更新/回滚固件，并通过 Windows 更新更新市场内设备。

- 支持开发固件/内置固件的灵活性。

- 能够将较大的固件映像分割为较小的段，使组件能够更轻松地接受固件映像。 

### <a name="122-non-goals"></a>1.2.2 非目标

- 定义固件映像的内部格式：对于主机，固件映像是一组地址和负载条目。

- 对接受的固件进行签名/加密/验证：此规范不介绍如何对固件映像进行签名和加密。 组件上运行的预期当前固件必须验证正在下载的固件。

- 定义有关组件如何与子组件进行交互的机制：主机作为单个单元与设备交互，通常是主组件。 组件必须充当与子组件固件相关的通信的桥。

## <a name="2-supported-hardware-architecture"></a>2支持的硬件体系结构

为了支持灵活的硬件设计，该协议支持多组件设备，其中每个组件都需要其自己的固件映像。 在设计中，一个组件是主组件，从属组件连接到该主组件。 每个组件都由组件 ID 唯一描述。  

作为单个单元，多组件设备对操作系统可见。 该主机仅与设备交互，通常是使用此 CFU 协议的主要组件。 组件与其子组件之间的通信超出了本规范的范围。  

在电脑上，可能有许多不同的设备 (设备中可能有一个或多个组件) 。 在此协议的上下文中，与每个设备之间的通信是独立的。 每个设备都有相应的主机实例。  

![设备固件、主组件及其子组件](images/primary-component.png)

## <a name="3-protocol-prerequisites"></a>3协议先决条件

本部分列出了利用此协议必须实现的必备和最佳实践：

- 原子映像使用情况

  在整个固件映像成功下载之前，不会使用组件的固件映像。 如果将固件拆分为多个段，则在从发送方接收最终段之前，不能使用映像。 必须对最终映像执行完整性检查。 建议使用传输来传送固件映像，并设置错误更正和重试机制，以避免发生传输错误时的重复下载。  

- 固件更新不得中断设备操作

  接受固件映像的设备必须能够在更新过程中运行。 设备必须有额外的内存用于存储和验证传入固件，而不覆盖其当前固件。  

- 身份验证和完整性

  实现器决定构成可信固件映像的因素。 建议组件的当前固件至少必须验证传入固件映像的 CRC。 当前固件还应使用数字签名或其他错误检测算法。 如果验证失败，则固件拒绝更新。 故障恢复

  如果固件映像已下载且不成功，则设备不得调用新的固件，并继续与现有固件一起操作。  主机可以重试更新。 重试频率是特定于实现的。

- 机密性

  可选。 可以加密固件段。 加密和解密技术超出了本规范的范畴。 此规范将固件负载视为数据流，无论其是否已加密。

- 回滚保护

  回滚策略由主要组件强制执行，并是特定于实现的。  组件上的当前固件根据内部策略验证传入的固件映像，例如版本号必须是较新的，或者无法从发布到调试等发布类型。 协议允许消息传递指示即使在违反回滚策略的情况，也会接受更新。

## <a name="4-cfu-protocol-overview"></a>4 CFU 协议概述

CFU 协议是一组命令和响应，将新的固件映像从主机 () 发送到要用于该固件的设备。

在高级别上，协议会循环访问所有要发送到设备的固件映像。 对于每个固件映像，主机 *提供* 将文件发送到设备。 仅当设备接受该产品/服务时，主机就会发送该文件。

若要支持设备更新顺序有依赖项的情况，设备可能不会在第一次传递中接受某些产品/服务，因此协议允许主机向设备重新发送所有固件服务，直到所有依赖项都得到解决。

### <a name="41-firmware-update-programming-command-sequence"></a>4.1 固件更新编程命令序列

下面是用于更新固件映像的 CFU 命令序列。

![固件更新编程命令序列](images/firmware-update-command-sequence.png)

#### <a name="411-state-host-initialized-notification"></a>4.1.1 状态：主机初始化通知

当主机自行初始化并标识了需要发送到设备的一组产品/服务后，主机将发出 "提供信息" " \_ \_ 启动 \_ 整个 \_ 事务" 命令，以向组件指示主机现在已初始化。 此命令的目的是通知当前设备固件，主机的新实例可用。 当主机的先前实例意外终止时，此通知很有用。 设备必须通过成功完成此命令。

#### <a name="412-state-offer_info_start_offer_list-notification"></a>4.1.2 状态：产品/服务 \_ 信息 \_ 开始 \_ 产品/服务 \_ 列表通知

在此状态下，主机会发出 "产品/服务" \_ \_ 启动 \_ 产品/服务 \_ 列表命令，指示它已准备好将产品/服务 () 发送到当前设备固件。 设备的主要组件必须通过成功完成此命令。

此命令非常有用，因为主机可能会多次向设备发送所有产品/服务。

#### <a name="413-state-send-firmware_update_offer-command"></a>4.1.3 状态：发送固件 \_ 更新 \_ 提供命令

主机会向主要组件 (或其子组件) 发送产品/服务，以检查组件是否要接受/拒绝固件。 此产品/服务包含有关固件映像的所有必要的元数据，因此该组件上的当前固件可以决定是接受、挂起、跳过还是拒绝该产品/服务。

此产品/服务可能适用于主要组件或子组件。 如果组件可以接受该产品/服务，它会自行准备好接收固件。 这可能包括准备内存 bank 来接收传入的固件映像。 组件可能不会接受该产品/服务，例如，该组件可能已具有主机要发送的更新 (或相同) 固件版本。 有关更多原因，请参阅附录1：示例固件更新编程命令序列中所述的示例。

即使接受了产品/服务，在下载的完整性和/或回滚检查发生故障后，主要组件仍可能会拒绝固件映像。 组件必须检查每个固件映像属性是否与产品/服务中的任何信息无关。

主机发出固件 \_ 更新产品/ \_ 服务命令，通知主要组件主机要发送的固件映像。

如果组件接受该产品/服务，则它具有固件 \_ 更新 \_ 提供 \_ 接受状态，因此接受该产品/服务。

如果设备固件处于繁忙状态，并且主组件目前无法接受此服务，或者当前提供了下一个产品/服务，则它将发送繁忙的响应，其中包含固件 \_ 更新 \_ 产品/服务的 \_ 忙状态。

如果当前固件对产品/服务感兴趣，但是不能接受该产品/服务 (例如，由于子组件缺少更新而导致的依赖项，因此) 它将使用固件 \_ 更新 \_ 产品/服务 " \_ 跳过"，指示它对此固件感兴趣，但是无法接受它。 然后，主机将继续执行下一个产品/服务，并且必须在以后重新提供此固件。

如果当前固件对产品/服务不感兴趣 (例如，它是较早版本) ，则它会使用 \_ \_ \_ 提供适当拒绝原因的固件更新提供拒绝状态进行响应。 此状态不表示在将来主机无法再发送此优惠。 通常，在每次将服务的列表初始化或重新发送到设备时，主机都会发送每个提议 (请参阅状态：产品/服务 \_ \_ 启动 \_ 产品/服务 \_ 列表通知) 。

#### <a name="414-state-send-firmware"></a>4.1.4 状态：发送固件

在此状态下，主机将开始向主组件发送固件映像，组件之前已接受该产品/服务。

由于固件映像的内容可能会超出单个命令的负载限制，因此主机会将固件映像分解为数据包。 主机按顺序在单独的固件更新内容命令中发送每个数据包 \_ 。 主组件必须生成每个命令的响应数据包。

每个固件 \_ 更新内容命令都说明了包含部分固件负载的偏移地址。 组件使用偏移量来确定必须将部分固件负载存储到的地址。 设备将内容写入适当的位置，并通过发送响应来确认命令。

对于主机发送的第一个数据包，它会设置固件 \_ 更新 \_ 标志 \_ 第一个 \_ 阻止标志，指示该设备是固件映像的第一个数据包。 如果设备尚未准备好接收固件，此时可能会执行此操作。

对于最后一个数据包，主机将发送，它会设置固件 \_ 更新 \_ 标志 \_ 最后一个 \_ 阻止标志。

设备上的当前固件已经编写了此命令中包含的部分固件负载后，在发送响应之前， *必须* 对传入固件映像执行验证和身份验证检查。 这至少包括：

- 验证整个固件映像的完整性的 CRC 检查。

- 如果 CRC 检查成功，则为传入映像的签名进行可选验证。

- 在可选签名检查后，版本检查以确保新固件版本与现有固件版本相同或更高。

如果传入固件映像分为较小段，则由当前固件确定，以确定它是否是固件映像的最后一段，并在验证过程中将所有段包括在内。

如果前面的检查通过，则当前固件可以将设备设置为在下次重置时交换到新映像，并将成功报告给主机。 通常，组件不启动自行重置。 这是为了防止与组件交互的任何软件、固件和硬件实体中断。 但是，这不是必需的，并且可能因实现而异。

如果验证步骤失败，固件必须在下一次重置时设置交换，并且必须指示对主机的失败响应。

#### <a name="415-decision-state-are-there-more-offers"></a>4.1.5 决策状态：是否有更多优惠

在此状态下，主机会确定是否有更多的产品/服务可发送到设备。

#### <a name="416-state-offer_info_end_offer_list-notification"></a>4.1.6 状态：提供 \_ 信息 \_ 结束 \_ 产品/服务 \_ 列表通知

当主机已将所有产品/服务发送到当前设备固件中的主要组件时，即达到此状态。 主机发送 "产品/服务" \_ \_ 端产品/服务 \_ \_ 列表命令，指示该服务已将所有产品/服务发送到组件。

设备必须通过成功完成此命令。

#### <a name="417-decision-state-replay-offer-list"></a>4.1.7 决策状态：重播提议列表

主机确定是否需要重新发送所有产品/服务。 如果以前的主组件跳过某些产品/服务并接受某些产品/服务，则可能会发生这种情况。 主机必须重新重播产品/服务列表。

可能存在其他特定于实现的逻辑，这可能会导致决定重播产品列表。

#### <a name="418-state-device-is-busy"></a>4.1.8 状态：设备繁忙

此状态表示设备返回对产品/服务的繁忙响应。

主机发送 "产品/ \_ 服务 \_ 通知 \_ 就绪" 命令，在设备可用之前，设备不会响应接受。

## <a name="5-cfu-protocol-packet-format"></a>5 CFU 协议数据包格式

CFU 协议是作为一组命令和响应实现的。 协议在本质上是连续的。 对于宿主发送到组件的每个命令，该组件都应该响应 (除非此规范中显式声明) 。 主机不会发送下一个命令，直到接收到其发送的上一个命令的有效响应。  

如果组件在某个时间段内未响应，或发送了无效的响应，则宿主可能会从头开始重新启动该进程。 此协议不会定义特定的超时值。  

可以通过命令获取组件上当前固件的版本信息;发送产品/服务并发送固件映像。

但是，主机不需要基于从主要组件收到的有关查询的版本信息的响应来预扣产品/服务。 此信息可用于日志记录或其他目的。

### <a name="51-get_firmware_version"></a>5.1 获取 \_ 固件 \_ 版本

获取主组件 (及其子组件) )  (的当前固件版本。 此命令不具有任何参数。

#### <a name="511-command"></a>5.1.1 命令

此命令由主机发送，用于查询主组件 (及其子组件) 上的当前固件 () ) 版本 (。 主机可以使用它来确认是否已成功更新固件。 收到此命令后，主要组件会对其自身和所有子组件的固件版本做出响应。

#### <a name="512-response"></a>5.1.2 响应

组件将以主组件和子组件的固件版本进行响应。 响应大小为60字节，允许最多七个组件的版本信息， (一个主组件和最多六个子组件) 。

###### <a name="table-51-1-get_firmware_version-response-layout"></a>表 5.1-1 GET_FIRMWARE_VERSION 响应布局

![GET_FIRMWARE_VERSION 响应布局](images/get-firmware-version-response-layout.png)

##### <a name="5121-header"></a>5.1.2.1 标头

###### <a name="table-51-2-get_firmware_version-response----header-layout"></a>表 5.1-2 GET_FIRMWARE_VERSION 响应头布局

![GET_FIRMWARE_VERSION 响应-标头布局](images/get-firmware-version-response-header-layout.png)

响应的标头提供以下信息。

###### <a name="table-51-3-get_firmware_version-response---header-bits"></a>表 5.1-3 GET_FIRMWARE_VERSION 响应头位

| 位偏移量 | 字段 | 大小 | 说明 |
|--|--|--|--|
| 0 | 组件计数 | 8 | 通过此组件由此机制管理的可下载组件数。 组件计数确定最大表大小。 当前支持最多7个组件，以确保响应可以在允许的60字节内容纳。 |
| 8 | 保留 | 16 | 保留的字段。 发件人必须将其设置为0。 接收方必须忽略此值。 |
| 24 | 协议版本 | 4 | 固件更新修订版本位表示目前正在传输中使用的 FW 更新协议修订版。 对于本文档中定义的接口，固件更新修订版本必须为0010b。 |
| 28 | 保留 | 3 | 保留的字段。 发件人必须将其设置为0。 接收方必须忽略此值。 |
| 31 | E | 1 | 扩展标志是将来用于启用附加组件的协议挂钩。 |

##### <a name="5122-component-version-and-properties"></a>5.1.2.2 组件版本和属性

对于每个组件，两个 Dword 用于描述最多7个组件的组件属性。 如果标头中的组件计数小于7，则响应末尾的未使用的 DWORD 必须设置为0。

###### <a name="table-51-4-get_firmware_version-response---component-version-and-properties-layout"></a>表 5.1-4 GET_FIRMWARE_VERSION 响应-组件版本和属性布局

![GET_FIRMWARE_VERSION 响应-组件版本和属性布局](images/get-firmware-version-response-component-version-and-properties-layout.png)

以下两个 Dword 中描述了每个组件的特定信息：

###### <a name="table-51-5-get_firmware_version-response---component-version-and-properties-bites"></a>表 5.1-5 GET_FIRMWARE_VERSION 响应-组件版本和属性片段

| 位偏移量 | 字段 | 大小 | 说明 |
|--|--|--|--|
| 0 | 固件版本 | 32 | 返回该组件当前固件的版本。 此规范不会对固件版本强制实施任何特定格式。 有关指南，请参阅固件版本部分。 |
| 32 | 银行 | 2 | 可选。 根据体系结构的不同，组件硬件可能有多个可以存储固件的银行。 根据实现，发送方可以指定固件当前所在的银行。 此字段是有条件的必需-支持是可选的，但是不能用于任何其他目的。 |
| 34 | 保留 | 2 | 保留的字段。 发件人必须将其设置为0。 接收方必须忽略此值。 |
| 36 | 特定于供应商 | 4 | 可用于实现特定方式的供应商特定字段。<br><br>供应商可以使用这些位来编码信息，如：<br><br>-固件类型：预发行/自主机/生产;调试/零售<br><br>-开发阶段<br><br>-Product ID，用于阻止组件使用同一更新协议接收其他产品的固件。 |
| 40 | 组件 ID | 8 | 组件的唯一标识符。 |
| 48 | 特定于供应商 | 16 | 可用于实现特定方式的供应商特定字段。 |

#### <a name="513-mapping-to-hid"></a>5.1.3 映射到 HID

此值作为 **HID Get 功能** 请求进行实现，该请求的响应大小为60字节，此外还有报表 ID。 功能报表长度适应整个获取 \_ 固件 \_ 版本响应。 没有与宿主获取功能请求关联的数据。

### <a name="52-firmware_update_offer"></a>5.2 固件 \_ 更新 \_ 产品/服务

确定主要组件是接受还是拒绝固件。

#### <a name="521-command"></a>5.2.1 命令

主机将此命令发送给组件，以确定它是接受还是拒绝固件。 主机必须发送产品/服务，并且组件必须接受该产品/服务，主机才能发送固件。

固件 \_ 更新 \_ 提供命令数据包的定义如下。

###### <a name="table-52-1-firmware_update_offer-command-layout"></a>表 5.2 FIRMWARE_UPDATE_OFFER 命令布局

![FIRMWARE_UPDATE_OFFER 命令布局](images/firmware-update-offer-command-layout.png)

##### <a name="5211-component-information"></a>5.2.1.1 组件信息

###### <a name="table-52-2-firmware_update_offer-command---component-information-layout"></a>表 5.2-2 FIRMWARE_UPDATE_OFFER 命令-组件信息布局

![FIRMWARE_UPDATE_OFFER 命令-组件信息布局](images/firmware-update-offer-command-component-information-layout.png)

此表描述了组件信息字节的位数。

###### <a name="table-52-3-firmware_update_offer-command---component-information-bits"></a>表 5.2 FIRMWARE_UPDATE_OFFER 命令-组件信息位

| 位偏移量 | 字段 | 大小 | 说明 |
|--|--|--|--|
| 0 | 段编号 | 8 | 此字段用于将组件的固件拆分为较小段的情况。 如果使用此值，则指示包含在后续负载数据包中的段。 例如，如果组件的固件映像非常大，并且主组件一次只能获取映像的较小部分，则此字段可用于指示此产品/服务适用于完成映像的 *第一段* 。 可以将单独的提议发送到包含图像的 *i* + n-1 段等的主要组件。 |
| 8 | 保留 | 6 | 保留的字段。 发件人必须将其设置为0。 接收方必须忽略此值。 |
| 14 | V | 1 | 强制忽略版本 (V) <br><br>-此标志用于预发布或调试固件映像。 它向组件表明，不基于固件版本拒绝固件。<br><br>-此标志用于开发阶段。 它可用于有意回滚到以前的固件版本。<br><br>-生产固件应忽略此标志。 |
| 15 | I | 1 | 强制立即重置 (我) <br><br>-此位值用于指示组件在固件下载完成并且经过验证后立即自动重置。<br><br>-此标志用于开发阶段。 |
| 16 | 组件 ID | 8 | 此字节用于多组件方案。 此字段可用于标识提供产品/服务的子组件。 如果未使用，则该值应为0。 组件 Id 的可能值如下：<br><br>1-0xDF：有效<br><br>0xE0-0xFD：保留。 请勿使用。<br><br>0xFF：产品/服务是一种特殊的产品/服务包。 有关详细信息，请参阅 FIRMWARE_UPDATE_OFFER 信息。<br><br>0xFE：产品/服务是一种特殊的优惠命令包。 有关详细信息，请参阅 FIRMWARE_UPDATE_OFFER 扩展部分。 |
| 24 | 令牌 | 8 | 该主机在 "产品/服务" 组件中插入唯一标记。 此令牌必须由提供响应中的组件返回。 <<br><br>如果需要组件区分主机的不同主机/类型，则此方法很有用。<br><br>要使用的确切值是特定于实现的。 例如，一个值可用于某个驱动程序，另一个用于应用程序。 这允许当前设备固件考虑 CFU 命令的可能多个发件人。 一个可能的实现可能是接受第一个 CFU 命令，并拒绝具有不同标记的所有其他命令，直到第一个 CFU 事务完成。 |

##### <a name="5212-firmware-version"></a>5.2.1.2 固件版本

这四个字节表示固件的32位版本。 此规范不会规定固件版本的格式。 建议使用以下项。

###### <a name="table-52-4-firmware_update_offer-command---firmware-version-layout"></a>表 5.2-4 FIRMWARE_UPDATE_OFFER 命令-固件版本布局

![FIRMWARE_UPDATE_OFFER 命令-固件版本布局](images/firmware-update-offer-command-firmware-version-layout.png)

此规范不会规定固件版本的格式，但以下是建议的指导原则。

###### <a name="table-52-5-firmware_update_offer-command---firmware-version-bits"></a>表 5.2-5 FIRMWARE_UPDATE_OFFER 命令-固件版本位

| 位偏移量 | 字段 | 大小 | 说明 |
|--|--|--|--|
| 0 | 变量 | 8 | 可对此字段进行描述，以区分预发行固件和生产固件。 它可能指示用于对固件进行签名的签名的类型。 |
| 8 | 次要版本 | 16 | 应为固件的每个版本更新此字段值。<br><br>应为固件的每个版本更新此字段值。 |
| 24 | 主要版本 | 8 | 此字段是固件映像的主版本。 在交付新的产品系列、固件的重大新更新等时，应更新此字段。 |

##### <a name="5213-vendor-specific"></a>5.2.1.3 供应商特定

这四个字节可用于对特定于供应商实现的产品/服务中的任何自定义信息进行编码。

##### <a name="5214-misc-and-protocol-version"></a>5.2.1.4 杂项协议版本

这四个字节可用于对特定于供应商实现的产品/服务中的任何自定义信息进行编码。

###### <a name="table-52-6-firmware_update_offer-command---vendor-specific-layout"></a>表 5.2-6 FIRMWARE_UPDATE_OFFER 命令特定于供应商的布局

![FIRMWARE_UPDATE_OFFER 命令-供应商特定布局](images/firmware-update-offer-command-vendor-specific-layout.png)

此表介绍了供应商特定字节的位数。

###### <a name="table-52-7-firmware_update_offer-command---misc-and-protocol-version"></a>表 5.2-7 FIRMWARE_UPDATE_OFFER 命令-其他和协议版本

| 位偏移量 | 字段 | 大小 | 说明 |
|--|--|--|--|
| 0 | 协议版本 | 4 | 必须将此字段设置为0010b，以指示主机/产品/服务对应于 CFU 协议的版本2。 |
| 4 | 保留 | 4 | 保留。 请勿使用。 |
| 8 | 保留 | 8 | 保留。 请勿使用。 |
| 16 | 特定于供应商 | 16 | 此字段可用于对特定于供应商实现的产品/服务中的任何自定义信息进行编码。 |

#### <a name="522-response"></a>5.2.2 响应

固件 \_ 更新 \_ 产品/服务的响应数据包的定义如下。

###### <a name="table-52-8-firmware_update_offer-response-token-layout"></a>表 5.2-8 FIRMWARE_UPDATE_OFFER 响应令牌布局

![FIRMWARE_UPDATE_OFFER 响应令牌布局](images/firmware-update-offer-response-token-layout.png)

##### <a name="5221-token"></a>5.2.2.1 标记

###### <a name="table-52-9-firmware_update_offer-response---token-layout"></a>表 5.2-9 FIRMWARE_UPDATE_OFFER 响应-令牌布局

![FIRMWARE_UPDATE_OFFER 响应令牌布局](images/firmware-update-offer-response-token-layout2.png)

此表描述了标记字节的位数。

###### <a name="table-52-10-firmware_update_offer-response---token-bits"></a>表 5.2-10 FIRMWARE_UPDATE_OFFER 响应-令牌位

| 位偏移量 | 字段 | 大小 | 说明 |
|--|--|--|--|
| 0 | 保留 | 8 | 保留。 请勿使用。 |
| 8 | 保留 | 8 | 保留。 请勿使用。 |
| 16 | 保留 | 8 | 保留。 请勿使用。 |
| 24 | 令牌 | 8 | 用于标识宿主的标记。 |

##### <a name="5222-reserved-b7---b4"></a>5.2.2.2 保留 (B7-B4) 

保留。 请勿使用。

##### <a name="5223-reject-reason-rr"></a>5.2.2.3 拒绝原因 (RR) 

###### <a name="table-52-11-firmware_update_offer-response---reject-reason-layout"></a>表 5.2-11 FIRMWARE_UPDATE_OFFER 响应-拒绝原因布局

![FIRMWARE_UPDATE_OFFER 响应-拒绝原因布局](images/firmware-update-offer-response-reject-reason-layout.png)

###### <a name="table-52-12-firmware_update_offer-response---reject-reason-bits"></a>表 5.2-12 固件 \_ 更新 \_ 提供响应-拒绝原因位

此表描述了拒绝原因字节的位数。

| 位偏移量 | 字段 | 大小 | 说明 |
|--|--|--|--|
| 0 | RR 代码 | 8 | 拒绝原因代码，指示组件提供的用于拒绝产品/服务的原因。 此值取决于状态字段。 有关状态到 RR 的代码映射，请参阅表 5.2-13。 |
| 8 | 保留 | 24 | 保留。 请勿使用。 |                                                             |

###### <a name="table-52-13-firmware_update_offer-response-rr-code-values"></a>表 5.2-13 固件 \_ 更新 \_ 提供响应 RR 代码值

此表描述了 RR Code 字节的可能值。

| RR 代码 | 名称 | 说明 |
|--|--|--|
| 0x00 | 固件 \_ 提议 \_ 拒绝 \_ 旧 \_ 固件 | 此产品/服务已被拒绝，因为提供的固件版本较旧或与当前固件相同。 |
| 0x01 | 固件 \_ 提议 \_ 拒绝 \_ INV \_ 组件 | 此产品/服务已被拒绝，因为提供的固件不适用于该产品的平台。 这可能是由不支持的组件 ID 导致的，或者提供的映像与系统硬件不兼容。 |
| 0x02 | 固件 \_ 更新 \_ 提供挂起的交换 \_ | 组件固件已更新，但交换到新固件处于挂起状态。 在交换完成之前，通常会通过重置完成固件更新处理。 |
| 0x03-0x08 |  (保留)  | 保留。 请勿使用。 |
| 0x09-0xDF |  (保留)  | 保留。 请勿使用。 |
| 0xE0-0xFF |  (供应商特定)  | 这些值由协议的设计器使用，表示特定于供应商。 |

##### <a name="5224-status"></a>5.2.2.4 状态

###### <a name="table-52-14-firmware_update_offer-response-status-layout"></a>表 5.2-14 FIRMWARE_UPDATE_OFFER 响应状态布局

![FIRMWARE_UPDATE_OFFER 响应状态布局](images/firmware-update-offer-response-status-layout.png)

此表描述了状态字节的位数。

###### <a name="table-52-15-firmware_update_offer-response---status-bits"></a>表 5.2-15 FIRMWARE_UPDATE_OFFER 响应-状态位

| 位偏移量 | 字段 | 大小 | 说明 |
|--|--|--|--|
| 0 | 状态 | 8 | 此值指示组件决定接受、挂起、跳过或拒绝该产品/服务。 组件提供 RR 代码字段值中的原因。 有关状态到 RR 的代码映射，请参阅表 5.2-16。 |
| 8 | 保留 | 24 | 保留。 请勿使用。 |

此表描述了状态字节的可能值。

###### <a name="table-52-16-firmware_update_offer-response-status-values"></a>表 5.2-16 FIRMWARE_UPDATE_OFFER 响应状态值

| 状态 | 名称 | 说明 |
|--|--|--|
| 0x00 | FIRMWARE_UPDATE_OFFER_SKIP | 组件已决定跳过该产品/服务。 主机必须在以后再次提供它。 |
| 0x01 | FIRMWARE_UPDATE_OFFER_ACCEPT | 组件决定接受该产品/服务。 |
| 0x02 | FIRMWARE_UPDATE_OFFER_REJECT | 组件已决定拒绝该产品/服务。 |
| 0x03 | FIRMWARE_UPDATE_OFFER_BUSY | 设备处于繁忙状态，主机必须等待设备准备就绪。 |
| 0x04 | FIRMWARE_UPDATE_OFFER_COMMAND | 当组件信息字节中的组件 ID (参阅5.1.2.1.1 组件信息) 设置为0xFE 时使用。<br><br>对于 "将命令代码设置为 OFFER_NOTIFY_ON_READY 请求"，指示附件已准备好接受其他产品。 |
| 0xFF | FIRMWARE_UPDATE_CMD_NOT_SUPPORTED | 无法识别产品/服务请求。 |

#### <a name="523-mapping-to-hid-protocol"></a>5.2.3 映射到 HID 协议

通过使用用于固件更新的专用 HID 实用程序报告 ID，使用 **Hid 输出报告** 机制向组件颁发消息。 要使用附录中描述的 HID 实用程序 TLC。

### <a name="53-firmware_update_offer---information"></a>5.3 固件 \_ 更新 \_ 提供-信息

如果组件信息字节中的组件 ID (参阅组件信息) 设置为0xFF，则会重新定义) 的位 (15 字节，以指示仅提供信息从主机到组件。 此机制允许可扩展性，并提供一种方式让主机向设备提供特定信息，如启动产品/服务、结束产品/服务列表、启动整个事务。 产品/服务信息数据包始终被组件立即接受。

#### <a name="531-command"></a>5.3.1 命令

固件 \_ 更新 \_ 产品/服务命令数据包定义如下：

###### <a name="table-53-1-firmware_update_offer---information-command-layout"></a>表 5.3-1 FIRMWARE_UPDATE_OFFER-信息命令布局

![FIRMWARE_UPDATE_OFFER-信息命令布局](images/firmware-update-offer-information-command-layout.png)

##### <a name="5311-component"></a>5.3.1.1 组件

###### <a name="table-53-2-firmware_update_offer---information-command---component-layout"></a>表 5.3-2 FIRMWARE_UPDATE_OFFER 信息命令-组件布局

![FIRMWARE_UPDATE_OFFER-Information 命令-组件布局](images/firmware-update-offer-information-command-component-layout.png)

此表中描述了组件字节的位数。

###### <a name="table-53-3-firmware_update_offer---information-command---component-bits"></a>表 5.3-3 FIRMWARE_UPDATE_OFFER 信息命令-组件位

| 位偏移量 | 字段 | 大小 | 说明 |
|--|--|--|--|
| 0 | 信息代码 | 8 | 此值指示信息的类型。 此值不是一个位掩码，并且只能是表 5.3-4 中描述的可能值之一。 |
| 8 | 保留。 | 8 | 保留。 请勿使用。 |
| 16 | 组件 ID | 8 | 设置为0xFF。 |
| 24 | 令牌 |  | 该主机在 "产品/服务" 组件中插入唯一标记。 此令牌必须由提供响应中的组件返回。 |

###### <a name="table-53-4-firmware_update_offer---information-command---information-code-values"></a>表 5.3-4 FIRMWARE_UPDATE_OFFER 信息命令-信息代码值

| 状态 | 名称 | 说明 |
|--|--|--|
| 0x00 | 产品/服务 \_ 信息 \_ 开始 \_ 整个 \_ 事务 | 指示主机是新主机，还是已被重新加载，整个产品/服务处理都 () 开始。 |
| 0x01 | 产品/服务 \_ 信息 \_ 开始 \_ 产品/服务 \_ 列表 | 指示当附件具有与确保在系统中的其他子组件之前更新一个子组件相关的下载规则时，主机中的产品/服务列表的开头。 |
| 0x02 | 产品/服务 \_ 信息 \_ 结束产品/服务 \_ \_ 列表 | 指示主机上的产品/服务列表的末尾。 |

##### <a name="5312-reserved-b7---b4"></a>5.3.1.2 保留 B7-B4

保留。 请勿使用。

##### <a name="5313-reserved-b11---b8"></a>5.3.1.3 Reserved B11-B8

保留。 请勿使用。

##### <a name="5314-reserved-b15---b12"></a>5.3.1.4 Reserved B15-B12

保留。 请勿使用。

#### <a name="532-response"></a>5.3.2 响应

固件 \_ 更新 \_ 产品/服务信息响应数据包回复定义如下。

###### <a name="table-53-5-firmware_update_offer---information-response-layout"></a>表 5.3-5 FIRMWARE_UPDATE_OFFER-信息响应布局

![FIRMWARE_UPDATE_OFFER-信息响应布局](images/firmware-update-offer-information-response-layout.png)

##### <a name="5321-token"></a>5.3.2.1 标记

###### <a name="table-53-6-firmware_update_offer--information-packet-response-token-layout"></a>表 5.3-6 FIRMWARE_UPDATE_OFFER-信息数据包响应令牌布局

![FIRMWARE_UPDATE_OFFER-信息数据包响应令牌布局](images/firmware-update-offer-information-packet-response-token-layout.png)

此表描述了标记字节的位数。

###### <a name="table-53-7-firmware_update_offer---information-response---token-bits"></a>表 5.3-7 FIRMWARE_UPDATE_OFFER 信息响应-令牌位

| 位偏移量 | 字段 | 大小 | 说明 |
|--|--|--|--|
| 0 | 保留 | 8 | 保留。 请勿使用。 |
| 8 | 保留 | 8 | 保留。 请勿使用。 |
| 16 | 保留 | 8 | 保留。 请勿使用。 |
| 24 | 令牌 | 8 | 用于标识主机的令牌 |

##### <a name="5322-reserved-b7---b4"></a>5.3.2.2 保留 B7-B4

保留。 请勿使用。

##### <a name="5323-reject-reason-rr"></a>5.3.2.3 拒绝原因 (RR) 

###### <a name="table-53-8-firmware_update_offer---information-response---rr-code-layout"></a>表 5.3-8 FIRMWARE_UPDATE_OFFER-信息响应-RR 代码布局

![FIRMWARE_UPDATE_OFFER-信息响应-RR 代码布局](images/firmware-update-offer-information-response-rr-code-layout.png)

此表描述了拒绝原因字节的位数。

###### <a name="table-53-9-firmware_update_offer--offer-information-response---rr-code-bits"></a>表 5.3-9 FIRMWARE_UPDATE_OFFER 提供信息响应-RR 代码位

| 位偏移量 | 字段 | 大小 | 说明 |
|--|--|--|--|
| 0 | RR 代码 | 8 | 拒绝原因代码，指示组件提供的用于拒绝产品/服务的原因。 表 5.3-10 中描述了可能的值。 此值取决于状态字段。 |
| 8 | 保留 | 24 | 保留。 请勿使用。 |

此表描述了 RR Code 字节的可能值。

###### <a name="table-53-10-firmware_update_offer--information-response---rr-code-values"></a>表 5.3-10 FIRMWARE_UPDATE_OFFER-信息响应-RR 代码值

| RR 代码 | 名称 | 说明 |
|--|--|--|
| 0x00 | 固件 \_ 提议 \_ 拒绝 \_ 旧 \_ 固件 | 此产品/服务已被拒绝，因为提供的固件版本较旧或与当前固件相同。 |
| 0x01 | 固件 \_ 提议 \_ 拒绝 \_ INV \_ 组件 | 此产品/服务已被拒绝，因为提供的固件不适用于该产品的平台。 这可能是由不支持的组件 ID 导致的，或者提供的映像与系统硬件不兼容。 |
| 0x02 | 固件 \_ 更新 \_ 提供挂起的交换 \_ | 组件固件已更新，但交换到新固件处于挂起状态。 在交换完成之前，通常会通过重置完成固件更新处理。 |
| 0x03-0x08 |  (保留)  | 保留。 请勿使用。 |
| 0x09-0xDF |  (保留)  | 保留。 请勿使用。 |
| 0xE0 —0xFF |  (供应商特定)  | 这些值由协议的设计器使用，表示特定于供应商。 |

##### <a name="5324-status"></a>5.3.2.4 状态

###### <a name="table-53-11-firmware_update_offer---offer-information-response-status-layout"></a>表 5.3-11 FIRMWARE_UPDATE_OFFER-产品/服务信息响应状态布局

![FIRMWARE_UPDATE_OFFER-产品信息响应状态布局](images/firmware-update-offer-offer-information-response-status-layout.png)

此表描述了状态字节的位数。

###### <a name="table-53-12-firmware_update_offer---offer-information---response-status-bits"></a>表 5.3-12 FIRMWARE_UPDATE_OFFER-产品/服务信息-响应状态位

| 位偏移量 | 字段 | 大小 | 说明 |
|--|--|--|--|
| 0 | 状态 | 8 | 必须将此字段设置为固件 \_ 更新 \_ 提供 \_ 接受。 这表示组件已决定接受该产品/服务。 |
| 8 | 保留。 | 24 | 保留。 请勿使用。 |

### <a name="54-firmware_update_offer---extended"></a>5.4 固件 \_ 更新 \_ 产品/服务-扩展

如果组件信息字节中的组件 ID 设置为0xFE，则会重新定义 bits (15 字节) ，以指示从主机到设备固件的 "提供" 命令。 此机制可用于向设备提供特定信息的可扩展性和方式。 当组件准备响应接受时，将返回 "产品/服务" 命令包。

#### <a name="541-command"></a>5.4.1 命令

如果组件信息字节中的组件 ID 设置为0xFE，则将重定义四个 Dword，如下所示：

###### <a name="table-54-1-firmware_update_offer---extended-command-layout"></a>表 5.4 FIRMWARE_UPDATE_OFFER 扩展命令布局

![FIRMWARE_UPDATE_OFFER 扩展命令布局](images/firmware-update-offer-extended-command-layout.png)

##### <a name="5411-component"></a>5.4.1.1 组件

###### <a name="table-54-2-firmware_update_offer---extended-command-packet---command---component-layout"></a>表 5.4-2 FIRMWARE_UPDATE_OFFER 扩展命令数据包布局

![FIRMWARE_UPDATE_OFFER 扩展命令数据包-命令组件布局](images/firmware-update-offer-extended-command-packet-command-component-layout.png)

此表中描述了组件字节的位数。

###### <a name="table-54-3-firmware_update_offer---extended-command---component-bits"></a>表 5.4 FIRMWARE_UPDATE_OFFER 扩展命令-组件位

| 位偏移量 | 字段 | 大小 | 说明 |
|--|--|--|--|
| 0 | 命令代码 | 8 | 此值指示命令的类型。 此值不是一个位掩码，并且只能是表 5.4-4 中描述的可能值之一。 |
| 8 | 保留。 | 8 | 保留。 请勿使用。 |
| 16 | 组件 ID | 8 | 设置为0xFE。 |
| 24 | 令牌 |  | 该主机在 "产品/服务" 组件中插入唯一标记。 此令牌必须由提供响应中的组件返回。 |

###### <a name="table-54-4-firmware_update_offer---extended-command---command-code-values"></a>表 5.4-4 FIRMWARE_UPDATE_OFFER 扩展命令-命令代码值

| 状态 | 名称 | 说明 |
|--|--|--|
| 0x01 | \_ \_ 在 \_ 准备就绪后提供通知 | 如果该产品/服务以前被组件拒绝，则由主机发送。 |
| 0x02-0xFF | 保留 | 保留 |

##### <a name="5412-reserved-b7---b4"></a>5.4.1.2 保留 B7-B4

保留。 请勿使用。

##### <a name="5413-reserved-b11---b8"></a>5.4.1.3 Reserved B11-B8

保留。 请勿使用。

##### <a name="5414-reserved-b15---b12"></a>5.4.1.4 Reserved B15-B12

保留。 请勿使用。

#### <a name="542-response"></a>5.4.2 响应

\_ \_ 可能无法立即接收来自设备的固件更新产品/服务命令响应。 响应的定义如下。

###### <a name="table-54-5-firmware_update_offer---extended-command-packet-response-layout"></a>表 5.4-5 FIRMWARE_UPDATE_OFFER 扩展命令数据包响应布局

![FIRMWARE_UPDATE_OFFER 扩展命令数据包响应布局](images/firmware-update-offer-extended-command-packet-response-layout.png)

##### <a name="5421-token"></a>5.4.2.1 标记

###### <a name="table-54-6-firmware_update_offer--offer-command-packet-response---token-layout"></a>表 5.4-6 FIRMWARE_UPDATE_OFFER 提供命令数据包响应-令牌布局

![FIRMWARE_UPDATE_OFFER 提供命令数据包响应-令牌布局](images/firmware-update-offer-offer-command-packet-response-token-layout.png)

此表描述了标记字节的位数。

###### <a name="table-54-7-firmware_update_offer---offer-command-response---token-bits"></a>表 5.4-7 FIRMWARE_UPDATE_OFFER 提供命令响应-令牌位

| 位偏移量 | 字段 | 大小 | 说明 |
|--|--|--|--|
| 0 | 保留 | 8 | 保留。 请勿使用。 |
| 8 | 保留 | 8 | 保留。 请勿使用。 |
| 16 | 保留 | 8 | 保留。 请勿使用。 |
| 24 | 令牌 | 8 | 用于标识宿主的标记。 |

##### <a name="5422-reserved-b7---b4"></a>5.4.2.2 保留 B7-B4

保留。 请勿使用。

##### <a name="5423-reject-reason"></a>5.4.2.3 拒绝原因

###### <a name="table-54-8-firmware_update_offer---offer-information-packet-response-rr-layout"></a>表 5.4-8 FIRMWARE_UPDATE_OFFER 提供信息数据包响应 RR 布局

![FIRMWARE_UPDATE_OFFER 提供信息数据包响应 RR 布局](images/firmware-update-offer-offer-information-packet-response-rr-layout.png)

此表描述了拒绝原因字节的位数。

###### <a name="table-54-9-firmware_update_offer--offer-command-response---rr-code"></a>表 5.4-9 FIRMWARE_UPDATE_OFFER 提供命令响应-RR 代码

| 位偏移量 | 字段 | 大小 | 说明 |
|--|--|--|--|
| 0 | RR 代码 | 8 | 此值取决于状态字段。 有关可能的 RR 代码值，请参阅表 5.4-10。 |
| 8 | 保留 | 24 | 保留。 请勿使用。 |

此表描述了 RR Code 字节的可能值。

###### <a name="table-54-10-firmware_update_offer--offer-command-packet---rr-code-values"></a>表 5.4 FIRMWARE_UPDATE_OFFER-提供命令数据包-RR Code 值

| RR 代码 | 名称 | 说明 |
|--|--|--|
| 0x00 | 固件 \_ 提议 \_ 拒绝 \_ 旧 \_ 固件 | 此产品/服务已被拒绝，因为提供的固件版本较旧或与当前固件相同。 |
| 0x01 | 固件 \_ 提议 \_ 拒绝 \_ INV \_ 组件 | 此产品/服务已被拒绝，因为提供的固件不适用于该产品的平台。 这可能是由不支持的组件 ID 导致的，或者提供的映像与系统硬件不兼容。 |
| 0x02 | 固件 \_ 更新 \_ 提供挂起的交换 \_ | 组件固件已更新，但交换到新固件处于挂起状态。 在交换完成之前，通常会通过重置完成固件更新处理。 |
| 0x03-0x08 |  (保留)  | 保留。 请勿使用。 |
| 0x09-0xDF |  (保留)  | 保留。 请勿使用。 |
| 0xE0 —0xFF |  (供应商特定)  | 这些值由协议的设计器使用，表示特定于供应商。 |

##### <a name="5424-status"></a>5.4.2.4 状态

###### <a name="table-54-11-firmware_update_offer---offer-command-packet-response-status-layout"></a>表 5.4 FIRMWARE_UPDATE_OFFER-提供命令数据包响应状态布局

![FIRMWARE_UPDATE_OFFER 提供命令数据包响应状态布局](images/firmware-update-offer-offer-command-packet-response-status-layout.png)

此表描述了状态字节的位数。

###### <a name="table-54-12-firmware_update_offer--offer-command-packet-response-rr-code"></a>表 5.4-12 FIRMWARE_UPDATE_OFFER 提供命令数据包响应 RR 代码

| 位偏移量 | 字段 | 大小 | 说明 |
|--|--|--|--|
| 0 | 状态 | 8 | 必须将此字段设置为固件 \_ 更新 \_ 提供 \_ 接受。 这表示组件已决定接受该产品/服务。 |
| 8 | 保留。 | 24 | 保留。 请勿使用。 |

### <a name="55-firmware_update_content"></a>5.5 固件 \_ 更新 \_ 内容

主机将此命令发送到设备固件，以提供固件内容 (即固件映像) 。 不应在单个命令中容纳整个映像文件。 主机必须将映像拆分为较小的块，每个命令一次发送一个图像块。

对于每个命令，主机都指示其他信息，无论是固件的第一个块、最后一个块还是如此。 设备固件的主要组件接受传入固件映像的每个块，将其存储在内存中，并且必须分别响应每个命令。

当主要组件收到最后一个块时，组件将验证整个固件映像 (CRC 检查、签名验证) 。 根据这些检查的结果，将为最后一个块返回相应的响应 (失败或成功) 。

#### <a name="551-command"></a>5.5.1 命令

###### <a name="table-55-1-firmware_update_content-command-layout"></a>表 5.5-1 FIRMWARE_UPDATE_CONTENT 命令布局

![FIRMWARE_UPDATE_CONTENT 命令布局](images/firmware-update-content-command-layout.png)

##### <a name="5511-header-b7---b0"></a>5.5.1.1 标头 (B7-B0) 

###### <a name="table-55-2-firmware_update_content-command-header-layout"></a>表 5.5-2 FIRMWARE_UPDATE_CONTENT 命令头布局

![FIRMWARE_UPDATE_CONTENT 命令头布局](images/firmware-update-content-command-header-layout.png)

\_此表描述了固件更新 \_ 内容标头的位数。

###### <a name="table-55-3-firmware_update_content-header-bits"></a>表 5.5-3 FIRMWARE_UPDATE_CONTENT 头位

| 位偏移量 | 字段 | 大小 | 说明 |
|--|--|--|--|
| 0 | Flags | 8 | 此字段提供有关命令的额外信息。 此值是用于数据传输的标志的掩码。 表 5.5-4 中描述了可能的值。 |
| 8 | 数据长度 | 8 | 适用的数据字段的长度，指示要写入的字节数。<br><br>根据此命令的大小，长度的最大允许值为52字节。 |
| 16 | 序列号 | 16 | 此值由主机创建，并且对于每个颁发的内容数据包都是唯一的。 组件必须返回其对此请求的响应中的序列号。 |
| 32 | 固件地址 | 32 | 小 Endian (LSB 首先) 用于写入数据的地址。 该地址是从0开始的。 在内存中放置图像时，固件会使用此偏移量来确定所需的地址。 |

此表描述了标志字节的可能值。

###### <a name="table-55-4-firmware_update_offer--offer-command-packet---flag-values"></a>表 5.5-4 FIRMWARE_UPDATE_OFFER 提供命令数据包标志值

| 标志 | 名称 | 说明 |
|--|--|--|
| 0x80 | FIRMWARE_UPDATE_FLAG_FIRST_BLOCK | 此标志指示这是固件映像的第一个块。 |
| 0x40 | FIRMWARE_UPDATE_FLAG_LAST_BLOCK | 此标志指示这是固件映像的最后一个块，映像已准备好进行验证。<br><br>在将此块写入非易失内存后，组件上的当前固件必须对整个下载的固件映像执行验证，这一点很重要。 |

##### <a name="5512-data"></a>5.5.1.2 数据

###### <a name="table-55-5-firmware_update_content-command-data-layout"></a>表 5.5-5 FIRMWARE_UPDATE_CONTENT 命令数据布局

![FIRMWARE_UPDATE_CONTENT 命令数据布局](images/firmware-update-content-command-data-layout.png)

\_此表介绍了固件更新 \_ 内容数据的位数。

###### <a name="table-55-6-firmware_update_content-command-data-bits"></a>表 5.5-6 FIRMWARE_UPDATE_CONTENT 命令数据位

| 位偏移量 | 字段 | 大小 | 说明 |
|--|--|--|--|
| 64 | 数据 | 最大52。 | 要写入的字节数组。 主机通常基于产品体系结构发送4个字节的块。 末尾的任何未使用的字节都必须填充0。 |

#### <a name="552-response"></a>5.5.2 响应

###### <a name="table-55-7-firmware_update_content-command-response-layout"></a>表 5.5-7 FIRMWARE_UPDATE_CONTENT 命令响应布局

![FIRMWARE_UPDATE_CONTENT 命令响应布局](images/firmware-update-content-command-response-layout.png)

##### <a name="5521-sequence-number"></a>5.5.2.1 序列号

###### <a name="table-55-8-firmware_update_content-response---sequence-number"></a>表 5.5-8 FIRMWARE_UPDATE_CONTENT 响应顺序号

![FIRMWARE_UPDATE_CONTENT 响应顺序号](images/firmware-update-content-response-sequence-number.png)

\_ \_ 此表介绍了 (3-0) 的固件更新内容响应的位数。

###### <a name="table-55-9-firmware_update_content---command---response-bits"></a>表 5.5-9 FIRMWARE_UPDATE_CONTENT 命令-响应位

| 位偏移量 | 字段 | 大小 | 说明 |
|--|--|--|--|
| 0 | 序列号 | 16 | 此字段是由请求中的主机发送的序列号。 |
| 16 | 保留 | 16 | 保留。 请勿使用。 |

##### <a name="5522-status"></a>5.5.2.2 状态

###### <a name="table-55-10-firmware_update_content-response-status-layout"></a>表 5.5-10 FIRMWARE_UPDATE_CONTENT 响应状态布局

![FIRMWARE_UPDATE_CONTENT 响应状态布局](images/firmware-update-content-response-status-layout.png)

\_ \_ 此表介绍了 (7-4) 的固件更新内容响应的位数。

###### <a name="table-55-11-firmware_update_offer---response---status-bits"></a>表 5.5-11 FIRMWARE_UPDATE_OFFER 响应-状态位

| 位偏移量 | 字段 | 大小 | 说明 |
|--|--|--|--|
| 0 | 状态 | 8 | 此值指示设备组件返回的状态代码。 这不是按位 "与" 表 5.5-12 中所述的值之一。 |
| 8 | 保留 | 24 | 保留。 请勿使用。 |

此表描述了状态字节的可能值。

###### <a name="table-55-12-firmware_update_offer--response---status-code-values"></a>表 5.5-12 FIRMWARE_UPDATE_OFFER 响应状态代码值

| 标志 | 名称 | 说明 |
|--|--|--|
| 0x00 | FIRMWARE_UPDATE_SUCCESS | 请求已成功完成。 |
| 0x01 | FIRMWARE_UPDATE_ERROR_PREPARE | 组件未准备好接收固件内容。<br><br>如果使用此代码，则通常在对第一个块的响应中使用。 例如，flash 上出现擦除错误。 |
| 0x02 | FIRMWARE_UPDATE_ERROR_WRITE | 请求无法写入字节。 |
| 0x03 | FIRMWARE_UPDATE_ERROR_COMPLETE | 请求无法将交换设置为响应 FIRMWARE_UPDATE_FLAG_LAST_BLOCK。 |
| 0x04 | FIRMWARE_UPDATE_ERROR_VERIFY | 对 DWORD 的验证失败，以响应 FIRMWARE_UPDATE_FLAG_VERIFY。 |
| 0x05 | FIRMWARE_UPDATE_ERROR_CRC | 固件映像的 CRC 未能响应 FIRMWARE_UPDATE_FLAG_LAST_BLOCK。 |
| 0x06 | FIRMWARE_UPDATE_ERROR_SIGNATURE | 固件签名验证失败，无法响应 FIRMWARE_UPDATE_FLAG_LAST_BLOCK。 |
| 0x07 | FIRMWARE_UPDATE_ERROR_VERSION | 固件版本验证失败，无法响应 FIRMWARE_UPDATE_FLAG_LAST_BLOCK。 |
| 0x08 | FIRMWARE_UPDATE_SWAP_PENDING | 已更新固件并等待交换。 重新设置附件之前，不能再接受固件更新命令。 |
| 0x09 | FIRMWARE_UPDATE_ERROR_INVALID_ADDR | 固件在消息数据内容中检测到无效的目标地址。 |
| 0x0A | FIRMWARE_UPDATE_ERROR_NO_OFFER | 接收到 FIRMWARE_UPDATE_OFFER 命令，但未首先接收到有效且接受的固件更新产品/服务。 |
| 0x0B | FIRMWARE_UPDATE_ERROR_INVALID | FIRMWARE_UPDATE_OFFER 命令的常规错误，如无效的适用数据长度。 |

##### <a name="5523-reserved-b8---b11"></a>5.5.2.3 Reserved B8-B11

保留。 请勿使用。

##### <a name="5524-reserved-b12---b15"></a>5.5.2.4 Reserved B12-B15

保留。 请勿使用。

## <a name="6-appendix-1-example-firmware-update-programming-command-sequence"></a>6附录1：固件更新编程命令序列示例

### <a name="61-example-1"></a>6.1 示例1

请考虑以下设备固件：

- 主组件-组件 ID 1-当前固件版本7.0。1

- 子组件-组件 ID 2-当前固件版本12.4.54

- 子组件-组件 ID 3-当前固件版本4.4。2

- 子组件-组件 ID 4-当前固件版本23.32。9

主机具有以下三个固件映像：  

- 组件 ID 1-固件版本7.1。3

- 组件 ID 2-固件版本12.4.54

- 组件 ID 3-固件版本4.5。0

序列将为：

1. 主机产品/服务：组件 ID 1-固件版本7.1。3

1. 主要组件接受产品/服务

1. 主机发送固件映像

1. 主组件接受固件，对其进行验证

1. 主机产品/服务：组件 ID 2-固件版本12.4.54

1. 主组件拒绝产品/服务

1. 主机产品/服务：组件 ID 3-固件版本4.5。0

1. 主要组件接受产品/服务

1. 主机发送固件映像

1. 主组件接受固件，对其进行验证

由于所有产品/服务都未被拒绝，主机会重播所有产品/服务：

1. 主机产品/服务：组件 ID 1-固件版本7.1。3

1. 组件拒绝

1. 主机产品/服务：组件 ID 2-固件版本12.4.54

1. 组件拒绝

1. 主机产品/服务：组件 ID 3-固件版本4.5。0

1. 组件拒绝

### <a name="62-example-2"></a>6.2 示例2

请考虑以下设备固件：

- 主组件-组件 ID 1-当前固件版本7.0。1

- 子组件-组件 ID 2-当前固件版本12.4.54

- 子组件-组件 ID 3-当前固件版本7.4。2

- 子组件-组件 ID 4-当前固件版本23.32。9

主机具有以下三个固件映像：  

- 组件 ID 1-固件版本8.0。0

- 组件 ID 2-固件版本12.4.54

- 组件 ID 3-固件版本9.0。0

此外，实现要求子组件的固件版本不得低于主组件上运行的固件版本。 宿主并不知道该要求，而是由主组件确定，以确保此规则。

序列将为：

1. 主机产品/服务：组件 ID 1-固件版本8.0。0

1. 由于尚未更新组件 ID 3，主组件拒绝 () 

1. 主机产品/服务：组件 ID 2-固件版本12.4.54

1. 主组件拒绝

1. 主机产品/服务：组件 ID 3-固件版本9.0。0

1. 主要组件接受提议

1. 主机发送固件映像

1. 主组件接受固件，对其进行验证

由于所有产品/服务都未被拒绝，主机会重播所有产品/服务

1. 主机产品/服务：组件 ID 1-固件版本8.0。0

1. 主要组件接受提议

1. 主机发送固件映像

1. 主组件接受固件，对其进行验证

1. 主机产品/服务：组件 ID 2-固件版本12.4.54

1. 主组件拒绝

1. 主机产品/服务：组件 ID 3-固件版本9.0。0

1. 主组件拒绝
