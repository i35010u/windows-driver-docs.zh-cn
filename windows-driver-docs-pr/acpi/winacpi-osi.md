---
title: 如何使用 _OSI 识别 ACPI 中的 Windows 版本
description: 提供了用来识别主机操作系统的 ACPI 源语言 (ASL) 操作系统接口级别 (\_OSI) 方法的信息。
ms.date: 11/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: c25144a88437574a1aae4b762e7a459b09637c88
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355797"
---
# <a name="how-to-identify-the-windows-version-in-acpi-by-using-osi"></a>如何使用 _OSI 识别 ACPI 中的 Windows 版本

本主题介绍如何使用\_OSI 方法在高级配置和电源接口 (ACPI) 源语言 (ASL) 标识的主机操作系统中。 通过使用此方法，ASL 编写器可以创建固件，以便支持将来的操作系统版本，并使操作系统更改基于请求的接口级别的行为。

此信息适用于以下操作系统：

- Windows 10 版本 1809
- Windows 10 版本 1803
- Windows 10 版本 1709
- Windows 10 版本 1703
- Windows 10 版本 1607
- Windows Server Technical Preview
- Windows 10
- Windows Server 2012 R2
- Windows 8.1
- Windows Server 2012
- Windows 8
- Windows Server 2008 R2
- Windows 7
- Windows Server 2008
- Windows Vista
- Windows Server 2003
- Windows XP

## <a name="the-osi-method"></a>\_OSI 方法

所有最新版本的 Windows 操作系统支持的组件[高级配置和电源接口 (ACPI) 规范](https://uefi.org/specifications)。 ACPI 规范定义了一种解释型的语言，ACPI 源语言 (ASL)，以便操作系统执行电源管理和配置提供固件控制方法。 若要提高 ASL 编写器来确定主机操作系统版本的功能，ASL 提供操作系统接口级别 (\_OSI)。

通过使用\_OSI 方法 ASL 编写器能够轻松确定的 ACPI 接口的主机操作系统支持的版本。 此版本控制方法提供一种解决方案用于创建可支持将来的操作系统，启用操作系统更改行为基于请求的接口级别的固件。

## <a name="osi-defined"></a>\_OSI 定义

\_OSI 方法都有一个自变量和一个返回值。 参数是一个字符串，以及每个操作系统进行定义。 如果支持该接口，则返回值是如果接口不支持 0x00000000 或 0xFFFFFFFF。

ACPI 规范的最新版本已扩展的用例\_OSI 超出主机操作系统版本标识的方法。 但是，Windows 支持\_OSI 仅供使用的标识系统运行的 Windows 的主机版本。

\_OSI 方法定义，如下所示：

- \\\_OSI-操作系统接口

### <a name="argument"></a>参数

一个字符串由定义并为每个操作系统。 例如：

- "Windows 2013"的 Windows 8.1 和 Windows Server 2012 R2
- Windows 8 和 Windows Server 2012 的"Windows 2012"
- "Windows 2009"的 Windows 7 和 Windows Server 2008 R2
- "Windows 2001"的 Windows XP
- 适用于 Windows Server 2003 的"Windows 2001.1"

### <a name="return-value"></a>返回值

返回值如下所示：

- 0x00000000 如果操作系统不支持的参数中的版本。
- 如果操作系统不支持版本的参数中，0xFFFFFFFF。

## <a name="osi-argument-details-for-windows"></a>\_OSI Windows 参数的详细信息

下表列出了的 ASL 可以确定通过使用相应的 Windows 版本\_OSI 字符串。

如果 Windows 操作系统返回 0xFFFFFFFF 参数\_OSI 方法指定早期版本的 Windows。 例如，Windows 7 返回这两个"Windows 2009"(Windows 7) 的 0xFFFFFFFF 和"Windows 2006"(Windows Vista)。

**\_对于 Windows 操作系统的 OSI 字符串**

| OSI 字符串          | 目标操作系统                     |
|---------------------|-------------------------------|
| Windows 2000        | Windows 2000                  |
| Windows 2001        | Windows XP                    |
| Windows 2001 SP1    | Windows XP SP1                |
| Windows 2001.1      | Windows Server 2003           |
| Windows 2001 SP2    | Windows XP SP2                |
| Windows 2001.1 SP1  | Windows Server 2003 SP1       |
| Windows 2006        | Windows Vista                 |
| Windows 2006 SP1    | Windows Vista SP1             |
| Windows 2006.1      | Windows Server 2008           |
| Windows 2009        | Windows 7, Win Server 2008 R2 |
| Windows 2012        | Windows 8, Win Server 2012    |
| Windows 2013        | Windows 8.1                   |
| Windows 2015        | Windows 10                    |
| Windows 2016        | Windows 10 版本 1607      |
| Windows 2017        | Windows 10 版本 1703      |
| Windows 2017.2      | Windows 10 版本 1709      |
| Windows 2018        | Windows 10 版本 1803      |
| Windows 2018.2      | Windows 10 版本 1809      |

### <a name="implementation-note"></a>实现说明

将标识中的操作系统的例程\_INI 方法下的\\ \_SB 作用域，以便\_OSI 可以尽早地运行。 此位置很重要，因为此操作系统会提供的功能基础的字符串参数\_OSI 方法。

## <a name="additional-resources"></a>其他资源
[高级的配置和电源接口规范](https://uefi.org/specifications)
