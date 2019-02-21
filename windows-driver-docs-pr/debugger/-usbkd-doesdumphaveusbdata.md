---
title: usbkd.doesdumphaveusbdata
description: Usbkd.doesdumphaveusbdata 命令检查以查看生成的崩溃转储文件中的哪些类型的 USB 数据作为结果的 Bug 检查 0xFE。
ms.assetid: 5E475E9F-BC8E-4185-9F63-5BAD49A83904
keywords:
- usbkd.doesdumphaveusbdata Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.doesdumphaveusbdata
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5e666bb7e3be9ac273da4b03f0bd974450217a37
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547985"
---
# <a name="usbkddoesdumphaveusbdata"></a>!usbkd.doesdumphaveusbdata


**！ Usbkd.doesdumphaveusbdata**命令检查，以了解哪些类型的 USB 数据所在的故障转储文件生成送[ **Bug 检查 0xFE**](bug-check-0xfe--bugcode-usb-driver.md)。

```dbgcmd
!usbkd.doesdumphaveusbdata
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="remarks"></a>备注
-------

使用此命令仅在调试时为生成的崩溃转储文件[ **Bug 检查 0xFE:BUGCODE\_USB\_驱动程序**](bug-check-0xfe--bugcode-usb-driver.md)。

<a name="examples"></a>示例
--------

下面是输出的示例 **！ doesdumphaveusbdata**

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






