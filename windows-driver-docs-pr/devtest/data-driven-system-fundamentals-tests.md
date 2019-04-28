---
title: 数据驱动的系统基础测试
description: 系统基础测试和 Windows 驱动程序相关的实用程序概述
keywords:
- Sysfund 测试
- 数据驱动的测试
ms.date: 06/28/2018
ms.localizationpriority: medium
ms.openlocfilehash: e66284eaf9a04f5e90af4c1d90ad81b7f601fb0d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356613"
---
# <a name="data-driven-system-fundamentals-tests"></a>数据驱动系统基础测试

从与企业 WDK (EWDK) 1703年开始，Microsoft 提供了可配置命令行版本的系统基础测试和相关的实用程序。  这些被称为"数据驱动"的测试和实用程序。

数据驱动的系统基础知识 (SysFund) 测试配置和自定义 XML 文件 (wdtftest.xml)，并通过命令行运行。 测试旨在运行尽早并经常在驱动程序和设备开发过程。

由于数据驱动的 SysFund 测试都是功能上等同于 SysFund 测试中 HLK，如果一个系统可以通过数据驱动的 SysFund 测试，它还应该能够通过 HLK SysFund 测试。 但是，与在 HLK SysFund 测试，不同的数据驱动 SysFund 测试都可配置为面向一组从一个设备在系统上所有设备的设备。  这允许为新的或更新设备和系统的一个迭代的测试过程。
