---
title: 如何使用 _OSI 识别 ACPI 中的 Windows 版本
description: 提供了用来识别主机操作系统的 ACPI 源语言 (ASL) 操作系统接口级别 (\_OSI) 方法的信息。
ms.date: 04/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4602a8fc145d9b64d5bf163f5aa46aa9900e1a81
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235369"
---
# <a name="how-to-identify-the-windows-version-in-acpi-by-using-_osi"></a>如何使用 _OSI 识别 ACPI 中的 Windows 版本

本主题介绍如何使用 \_ 高级配置和电源接口（ACPI）源语言（ASL）中的 OSI 方法来识别主机操作系统。 通过使用此方法，ASL 编写器可以创建支持将来操作系统版本的固件，并使操作系统能够根据请求的接口级别更改行为。

此信息适用于以下操作系统：

- Windows 10 版本2004
- Windows 10 版本 1903
- Windows 10 版本 1809
- Windows 10 版本 1803
- Windows 10 版本 1709
- Windows 10 版本 1703
- Windows 10 版本 1607
- Windows Server Technical Preview
- Windows 10
- Windows Server 2012 R2
- Windows 8.1
- Windows Server 2012
- Windows 8
- Windows Server 2008 R2
- Windows 7
- Windows Server 2008
- Windows Vista
- Windows Server 2003
- Windows XP

## <a name="the-_osi-method"></a>\_OSI 方法

所有最新版本的 Windows 操作系统都支持[高级配置和电源接口（ACPI）规范](https://uefi.org/specifications)的组件。 ACPI 规范定义一种解释型语言（ACPI 源语言（ASL）），以使操作系统能够为电源管理和配置执行固件提供的控制方法。 为了改善 ASL 编写器识别主机操作系统版本的能力，ASL 提供了操作系统接口级别（ \_ OSI）。

通过使用 \_ OSI 方法，ASL 编写器可以轻松确定主机操作系统支持的 ACPI 接口版本。 此版本控制方法为创建固件提供了一个解决方案，该解决方案可支持将来的操作系统，并使操作系统能够根据请求的接口级别更改行为。

## <a name="_osi-defined"></a>\_已定义 OSI

\_OSI 方法具有一个参数和一个返回值。 参数是为每个操作系统定义的字符串。 如果接口不受支持，则返回值为 0x00000000; 如果支持接口，则为0xFFFFFFFF。

最新版本的 ACPI 规范已经扩展了 OSI 方法的用例， \_ 超出了主机操作系统版本标识。 但是，Windows \_ 只支持使用 OSI 来识别在系统上运行的 Windows 的主机版本。

\_OSI 方法定义如下：

- \\\_OSI-操作系统接口

### <a name="argument"></a>参数

为每个操作系统定义的一个字符串。 例如：

- 适用于 Windows 8.1 和 Windows Server 2012 R2 的 "windows 2013"
- 适用于 Windows 8 和 Windows Server 2012 的 "windows 2012"
- 适用于 Windows 7 和 Windows Server 2008 R2 的 "windows 2009"
- Windows XP 的 "windows 2001"
- Windows Server 2003 的 "windows 2001.1"

### <a name="return-value"></a>返回值

返回值如下所示：

- 0x00000000 （如果操作系统不支持参数中的版本）。
- 如果操作系统支持参数中的版本，则为0xFFFFFFFF。

## <a name="_osi-argument-details-for-windows"></a>\_Windows 的 OSI 参数详细信息

下表列出了 ASL 可以通过使用相应的 OSI 字符串来识别的 Windows 版本 \_ 。

如果 \_ OSI 方法的参数指定较早版本的 windows，则 Windows 操作系统返回0xffffffff。 例如，Windows 7 同时为 "Windows 2009 （Windows 7）" 和 "Windows 2006" （Windows Vista）返回0xFFFFFFFF。

### <a name="_osi-strings-for-windows-operating-systems"></a>\_适用于 Windows 操作系统的 OSI 字符串

| OSI 字符串          | 目标操作系统                     |
|---------------------|-------------------------------|
| Windows 2000        | Windows 2000                  |
| Windows 2001        | Windows XP                    |
| Windows 2001 SP1    | Windows XP SP1                |
| Windows 2001。1      | Windows Server 2003           |
| Windows 2001 SP2    | Windows XP SP2                |
| Windows 2001.1 SP1  | Windows Server 2003 SP1       |
| Windows 2006        | Windows Vista                 |
| Windows 2006 SP1    | Windows Vista SP1             |
| Windows 2006。1      | Windows Server 2008           |
| Windows 2009        | Windows 7、Win Server 2008 R2 |
| Windows 2012        | Windows 8，Win Server 2012    |
| Windows 2013        | Windows 8.1                   |
| Windows 2015        | Windows 10                    |
| Windows 2016        | Windows 10 版本 1607      |
| Windows 2017        | Windows 10 版本 1703      |
| Windows 2017。2      | Windows 10 版本 1709      |
| Windows 2018        | Windows 10 版本 1803      |
| Windows 2018。2      | Windows 10 版本 1809      |
| Windows 2019        | Windows 10 版本 1903      |
| Windows 2020        | Windows 10 版本2004      |

### <a name="implementation-note"></a>实现注释

将标识操作系统的例程置于 \_ SB 范围内的某个 INI 方法中， \\ \_ 以便 \_ OSI 可以尽早运行。 此位置很重要，因为操作系统会根据 OSI 方法的字符串参数提供功能 \_ 。

## <a name="additional-resources"></a>其他资源

[高级配置和电源接口规范](https://uefi.org/specifications)
