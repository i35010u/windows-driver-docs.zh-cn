---
title: 按钮行为
description: 本主题描述硬件按钮的预期行为。
ms.assetid: 057A4F21-3514-4CCA-BCE2-279E8228B5A9
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fc892b12dbe6963435000f3e1bde8d3998771fa9
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381387"
---
# <a name="button-behavior"></a>按钮行为

本主题描述硬件按钮的预期行为。

## <a name="required-and-optional-buttons-in-windows10"></a>Windows 10 中的 "必需" 和 "可选" 按钮

|操作系统/设备|电源|增加/减少音量|开始|返回/搜索|照相机|旋转锁定|
|---|---|---|---|---|---|---|
|Windows 10 移动版|必需|必选|对于使用 WVGA 显示的手机是必需的。 对于所有其他设备来说为可选|对于使用 WVGA 显示的手机是必需的。 对于所有其他设备来说为可选|可选|不支持|
|适用于桌面版的 Windows 10 (家庭版、专业版、企业版和教育版) /Tablets|必选|必需|可选|不支持|不支持|可选|
|适用于桌面版/其他设备的 Windows 10|必需|使用可拆卸键盘的设备所必需。 对于所有其他设备是可选的。|可选|不支持|不支持|可选|

有关按钮要求的详细信息：

- 对于 Windows 10 移动版，请参阅 [最低硬件要求](/windows-hardware/design/minimum/minimum-hardware-requirements-overview)中的2.6 节。
- 对于桌面版的 Windows 10，请参阅 [最低硬件要求](/windows-hardware/design/minimum/minimum-hardware-requirements-overview)中的3.6 节。

## <a name="button-behavior-in-windows10"></a>Windows 10 中的按钮行为

### <a name="single-button-behavior-in-windows10"></a>Windows 10 中的单个按钮行为

|Button|活动|Windows 10 桌面版|Windows 10 移动版|
|---|---|---|---|
|电源|按下并释放|开启/关闭开关|开启/关闭开关|
|电源|长按|启动关机窗帘|启动关机窗帘|
|电源|长按下并保持|硬关机|硬件重置|
|搜索|按下并释放|不支持|在启用的市场中启动 Cortana () /Search|
|搜索|长按|不支持|启动 Cortana 或通过语音进行搜索|
|调高音量|按下并释放|递增量|递增量|
调高音量|长按|自动重复卷增量|自动重复卷增量|
|减小音量|按下并释放|减量卷|减量卷|
|减小音量|长按|自动重复卷递减|自动重复卷递减|
|返回|按下并释放|上一个应用页面/关闭应用|上一个应用页面/关闭应用|
|返回|长按|启动任务切换器|启动切换器 UI|
|开始||切换开始屏幕|显示开始屏幕|
|旋转锁定||不支持|不支持 (有一个 UI 选项) |
|相机焦点||启动照相机应用程序|由相机应用处理 (焦点) |
|照相机快门||由相机应用程序处理|启动相机应用/拍照|

### <a name="button-combination-behavior-in-windows10"></a>Windows 10 中的按钮组合行为

如上所述，Windows 10 中的一些按钮组合适用于 [windows 10 按钮体系结构](../hid/buttons.md) 或 Windows 8.1 按钮体系结构。 Windows 10 中的所有其他按钮组合适用于这两种按钮体系结构。 建议使用 Windows 10 体系结构描述硬件按钮。

|按钮组合|Windows 10 桌面版|Windows 10 移动版|
|---|---|---|
|启动 + 向上音量|切换屏幕讲述人|切换屏幕讲述人 (是否已启用相应的 "轻松访问" 设置) |
|开始和音量降低|拍摄屏幕截图|不支持|
|开始 + 电源|仅当使用 Windows 8.1 按钮体系结构时，Ctrl + Alt + Del () |不支持|
|接通电源 + 音量|仅在使用 Windows 10 按钮体系结构) 时获取屏幕截图 (|拍摄屏幕截图|
|幂 + 向下音量|仅当使用 Windows 10 按钮体系结构时，Ctrl + Alt + Del () |启动 Windows 反馈应用。 10秒钟后 (硬件重置) |

## <a name="button-behavior-in-windows-81"></a>Windows 8.1 中的按钮行为

### <a name="single-button-behavior-in-windows-81"></a>Windows 8.1 中的单个按钮行为

|Button|操作|Windows 8.1|Windows 8.1 电话|
|---|---|---|---|
|电源|按下并释放|开启/关闭开关|开启/关闭开关|
|电源|长按|启动关机窗帘|启动关机窗帘|
|电源|长按下并保持|硬关机|硬件重置|
|搜索|按下并释放|不支持|启动 Cortana|
|搜索|长按|不支持|通过语音启动 Cortana|
|调高音量|按下并释放|递增量|递增量|
|调高音量|长按|自动重复卷增量|自动重复卷增量|
|减小音量|按下并释放|减量卷|减量卷|
|减小音量|长按|自动重复卷递减|自动重复卷递减|
|返回||不支持|不支持|
|开始||切换开始屏幕|切换开始屏幕|
|旋转锁定||Release：锁定旋转|锁定旋转|
|相机焦点||不支持|不适用|
|照相机快门||不支持|不适用|

### <a name="button-combination-behavior-in-windows-81"></a>Windows 8.1 中的按钮组合行为

|按钮组合|Windows 8.1|Windows 8.1 电话|
|---|---|---|
|启动 + 向上音量|切换屏幕讲述人|不支持|
|开始和音量降低|拍摄屏幕截图|不支持|
|开始 + 电源|Ctrl+Alt+Del|不支持|
|接通电源 + 音量|不支持|拍摄屏幕截图|
|幂 + 向下音量|不支持|10秒钟后 (硬件重置) |

## <a name="related-topics"></a>相关主题

[Windows 10 按钮体系结构](../hid/buttons.md)  
[最低硬件要求](/windows-hardware/design/minimum/minimum-hardware-requirements-overview)