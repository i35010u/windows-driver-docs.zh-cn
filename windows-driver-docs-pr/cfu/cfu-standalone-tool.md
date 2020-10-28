---
title: 组件固件更新 (CFU) 独立工具
description: 提供有关组件固件更新的信息 (CFU) 独立工具，该工具可将固件更新映像文件发送到设备。
ms.date: 10/01/2020
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: 06adbb8e9a34b2f46be1d0a381243102b89d741e
ms.sourcegitcommit: eefc6ae6d9621d0735b3c63e718ee5838d57a6bc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92886316"
---
# <a name="component-firmware-update-cfu-standalone-tool"></a>组件固件更新 (CFU) 独立工具

[CFU 独立工具](https://github.com/microsoft/CFU/tree/master/Tools/ComponentFirmwareUpdateStandAloneToolSample)将固件映像更新文件发送到设备。 在开发过程中，可以使用它在设备上测试固件更新，并将其上载到 Windows 更新。

. 在发送固件映像之前，该工具会将多个命令发送到带有固件提供的设备。 仅当设备接受时，该工具将发送固件负载。 工具与设备之间的通信依照 [CFU 协议](cfu-specification.md)，一种开放源规范 (包含在 CFU) 中（基于 HID 协议）。

此工具读取一个产品/服务文件并将固件更新映像文件传递到设备。  它还能够根据协议设置和请求/打印固件版本信息搜索设备。

它要求将协议设置文本 .csv 文件作为参数进行传递。

## <a name="tool-usage-command-format-examples"></a>工具用法命令格式示例

```console
FwUpdateCfu.exe version \<protocolSettingsPath\> (to retrieve version of device)
```

```console
FwUpdateCfu.exe update \<protocolSettingsPath\> \<offerfile\> \<binfile\> [forceIgnoreVersion] [forceReset]
```

## <a name="example-protocol-settings-in-csv-file"></a>.Csv 文件 (的示例协议设置) 

```text
#instructions:
#Fill in csv tag and the value in hex for each item
#order not important
#only the first 2 fields will be looked at so values after that are considered comments
VID,0x045e,#mandatory (each vendor must maintain their own Vendor defined Utility Page collections)
PID,0x07cd,#optional
USAGEPAGE,0xFF07,#mandatory (each vendor must maintain their own Vendor defined Utility Page collections)
USAGECOLLECTION,0x31,#optional (if you don't specify, the tool will attempt to talk to all devices with matching UsagePage/Vid/Pid on the usages specified below)
VERSION_FEATURE_USAGE,0x62,#mandatory for all procedures
CONTENT_OUTPUT_USAGE,0x61,#mandatory for fwUpdate procedure
CONTENT_RESPONSE_INPUT_USAGE,0x66,#mandatory for fwUpdate procedure
OFFER_OUTPUT_USAGE,0x8e,#mandatory for fwUpdate procedure
OFFER_RESPONSE_INPUT_USAGE,0x8a,#mandatory for fwUpdate procedure
```
