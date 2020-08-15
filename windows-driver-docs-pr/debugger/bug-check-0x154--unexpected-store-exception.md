---
title: Bug 检查 0x154 UNEXPECTED_STORE_EXCEPTION
description: UNEXPECTED_STORE_EXCEPTION bug 检查的值为0x00000154。 这表示内核内存存储组件捕获到意外异常。
ms.assetid: 5D51212E-459C-4F58-9321-5E55FD793401
keywords:
- Bug 检查 0x154 UNEXPECTED_STORE_EXCEPTION
- UNEXPECTED_STORE_EXCEPTION
ms.date: 02/27/2020
topic_type:
- apiref
api_name:
- UNEXPECTED_STORE_EXCEPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dfb6fc82931517ade32f0e06563614b8c1450fc2
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252979"
---
# <a name="bug-check-0x154-unexpected_store_exception"></a>Bug 检查0x154：意外的 \_ 存储 \_ 异常

意外的 \_ 存储 \_ 异常 bug 检查的值为0x00000154。 这表示内核内存存储组件捕获到意外异常。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅 [排查蓝屏错误](https://www.windows.com/stopcode)。

## <a name="unexpected_store_exception-parameters"></a>意外的 \_ 存储 \_ 异常参数

| 参数 | 描述                                  |
|-----------|----------------------------------------------|
| 1         | 指向存储区上下文或数据管理器的指针 |
| 2         | 异常信息                        |
| 3         | 保留                                     |
| 4         | 保留                                     |

## <a name="resolution"></a>解决方法

确定此问题的原因通常需要使用调试器来收集其他信息。 应该检查多个转储文件，以查看此 stop 代码是否具有类似的特征，例如，在出现 stop 代码时是否运行相同的代码。 有关详细信息，请参阅使用[Windows 调试器的故障转储分析 (WinDbg) ](crash-dump-files.md)[使用！分析扩展](using-the--analyze-extension.md)和[！分析](-analyze.md)。

如果有关于相关源代码的信息可用，则在执行此代码之前，请在相关代码中设置一个断点，然后在代码中执行一步操作，以查看用于控制代码流的关键变量的值。  仔细检查代码区域，查找错误假设或其他错误。

## <a name="troubleshooting-tips"></a>故障排查提示

如果无法处理导致此问题的基本代码，这些故障排除提示可能会有所帮助。

- 检查中的系统日志事件查看器是否有其他错误消息，这些错误消息可能有助于找出导致错误的设备或驱动程序。 若要打开事件查看器选择键盘快捷方式 Win + R，键入 `eventvwr.msc` 并按 enter 键。 在与蓝色屏幕相同的时间范围内查找系统日志中的严重错误。

- 选择 "开始"，在搜索框中键入 **"Windows 内存诊断"** ，然后按 enter。 选择是否重新启动计算机并立即运行该工具，或计划在下次重新启动时运行该工具。 Windows 内存诊断在计算机重新启动后自动运行，并自动执行标准内存测试。 若要运行扩展测试，请按 F1，并使用向上键和向下键将测试组合设置为 "扩展"，然后按 F10 应用所需的设置并恢复测试。

- 查看设备管理器查看是否有任何设备标记为惊叹号 (！ ) 。 查看在驱动程序属性中显示的任何错误驱动程序的事件日志。 请尝试更新相关驱动程序。

- 使用系统文件检查器工具修复丢失或损坏的系统文件。 系统文件检查器是 Windows 中的一个实用工具，它允许用户在 Windows 系统文件中扫描损坏并还原损坏的文件。 使用以下命令 ( # A0) 运行系统文件检查器工具。

  `SFC /scannow`

   有关详细信息，请参阅 [使用系统文件检查器工具修复丢失或损坏的系统文件](https://support.microsoft.com/help/929833/use-the-system-file-checker-tool-to-repair-missing-or-corrupted-system)。

