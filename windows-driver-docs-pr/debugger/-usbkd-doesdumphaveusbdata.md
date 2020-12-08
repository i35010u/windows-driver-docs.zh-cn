---
title: usbkd.doesdumphaveusbdata
description: Usbkd. doesdumphaveusbdata 命令将检查哪些类型的 USB 数据在崩溃转储文件中，该文件是由 Bug 检查0xFE 生成的。
keywords:
- usbkd doesdumphaveusbdata Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.doesdumphaveusbdata
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b6fc6fe633d51424f81ba5d2882868e2bc2033cc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816989"
---
# <a name="usbkddoesdumphaveusbdata"></a>!usbkd.doesdumphaveusbdata


**！ Usbkd doesdumphaveusbdata** 命令将检查哪些类型的 USB 数据在崩溃转储文件中，该文件是在 [**错误检查 0xFE**](bug-check-0xfe--bugcode-usb-driver.md)的结果中生成的。

```dbgcmd
!usbkd.doesdumphaveusbdata
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="remarks"></a>备注
-------

仅当调试因 [**Bug 检查0xFE： BUGCODE \_ USB \_ 驱动程序**](bug-check-0xfe--bugcode-usb-driver.md)而生成的故障转储文件时，才使用此命令。

<a name="examples"></a>示例
--------

下面是 **！ doesdumphaveusbdata** 的输出示例

```dbgcmd
1: kd> !analyze -v
*** ...
BUGCODE_USB_DRIVER (fe) 
...
1: kd> !usbkd.doesdumphaveusbdata

Retrieving crashdump information Please Wait...

Checking for GuidUsbHubPortArrayData information...
There is no data for this GUID in the mini dump.
No data to print  

Checking for GuidUsbHubExt information...
There is no data for this GUID in the mini dump.
No data to print  

Checking for GuidUsbPortLog information...
GuidUsbPortLog Exists with PORT Log Size = 8000 

Checking for GuidUsbPortContextData information...
GuidUsbPortContextData Exists with Data Length = 4c8 

Checking for GuidUsbPortExt information...
GuidUsbPortExt Exists (DEVICE_EXTENSION + DeviceDataSize ) = 2250
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

