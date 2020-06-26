---
title: CGMS-A 标准
description: CGMS-A 标准
ms.assetid: e41de08f-4dfa-42fc-8ddb-f27385c5780a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a92660ba8bd0c06071295c94ab0df5bbfe325c2
ms.sourcegitcommit: df7d6565a4cd2659c46d5fd83ef04a1672c60dbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382736"
---
# <a name="cgms-a-standards"></a>CGMS-A 标准

复制生成管理系统-模拟（CGMS）是用于模拟视频信号的复制保护系统。 各个国家和地区使用不同版本的 CGMS。 硬件供应商必须确保其显示微型端口驱动程序支持适当的 CGMS 版本。

例如，要在日本使用的图形适配器的驱动程序可能支持关联无线电行业和企业（ARIB） B15 standard，这是数字卫星广播的操作指导原则。 但是，要在美国中使用的图形适配器的驱动程序应支持国际电工委员会（IEC）61880标准或使用者电子设备协会（CEA） CEA 608-B 标准。 图形适配器的显示微型端口驱动程序支持的标准取决于适配器传输的信号类型。

以下列表描述了定义 CGMS 的各种标准。 仅在 CEA-805-标准中定义了再分发控制。

- **CEA-805-A**
  - 组件视频接口上的数据
  - 定义 CGMS 和再发行控制信息应如何编码为模拟480p、720p 或1080i 信号，该信号是从组件视频输出（Y/Pb/Pr 输出）传输的。
  - 此标准由[消费电子设备协会（CEA）](https://www.standardsportal.org/usa_en/sdo/cea.aspx)发布。

- **CEA-608-B 和 EIA-608-B**
  - 第21行数据服务
  - 定义如何在通过 RF、复合或 S 视频输出传输的480i 信号中对 CGMS 信息进行编码。
  - 此标准由 CEA 和[电子组件行业协会](https://go.microsoft.com/fwlink/p/?linkid=71278)（ECIA）发布。

- **EN 300 294 1.3.2 （1998-04）**
  - 电视系统;625线电视-宽屏幕信号（WSS）
  - 定义如何在576i 阶段替换行（PAL）中或使用内存（SECAM）信号的有序颜色对 CGMS 进行编码。
  - 此标准由[欧洲电信标准协会](https://go.microsoft.com/fwlink/p/?linkid=26364)（ETSI）发布。

- **IEC-61880-第一版-视频系统（525/60）**  
  - 使用垂直消隐间隔模拟接口的视频和附带数据
  - 编码 CGMS 的一种方法，即480i 视频信号中的信息，通过模拟或数字视频输出传输。
  - 此方法由[国际电工委员会](https://go.microsoft.com/fwlink/p/?linkid=8732)（IEC）发布。

- **IEC-61880-2-第一版-视频系统（525/60）**
  - 视频和附带的数据使用垂直消隐间隔-模拟接口-第 2: 525 部分的渐进扫描系统
  - 编码 CGMS 的一种方法，即480p 视频信号中的信息，通过模拟或数字视频输出传输。

- **IEC-62375-视频系统（625/50 渐进式）**
  - 使用垂直消隐间隔模拟接口的视频和附带数据
  - 编码 CGMS 的一种方法，即576p 视频信号中的信息，通过模拟或数字视频输出传输。

- **ARIB TR-B15**
  - 数字卫星广播的操作指导原则
  - 定义如何在通过视频输出传输的模拟480i、480p、720p 或1080i 信号中对 CGMS 信息进行编码。
  - 此标准仅适用于日本。
  - 此标准由[广播行业和企业的关联](https://go.microsoft.com/fwlink/p/?linkid=71283)（ARIB）发布。
