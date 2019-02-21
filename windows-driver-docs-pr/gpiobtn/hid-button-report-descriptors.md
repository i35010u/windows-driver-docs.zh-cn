---
title: HID 的按钮报告描述符
description: 本主题包含示例 HID 按钮报告描述符。
ms.assetid: FB1D482A-A147-4362-969F-7A37E5ECF0B4
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 48dc708730e7069639a18d0478fba5ded495d457
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525031"
---
# <a name="hid-button-report-descriptors"></a>HID 的按钮报告描述符


本主题包含示例 HID 按钮报告描述符。

``` syntax
0x05, 0x01,                  // USAGE_PAGE (Generic Desktop)
0x09, 0x06,                 // USAGE (Keyboard)
0xa1, 0x01,                 // COLLECTION (Application)
0x85, REPORTID_KEYBOARD,      // REPORT_ID
0x05, 0x07,                 // USAGE_PAGE (Key Codes)
0x09, 0x4c,                 // USAGE (Del Key)
0x09, 0x69,                 // USAGE (F14 Key)
0x09, 0x6a,                 // USAGE (F15 Key)
0x09, 0xe0,                 // USAGE (Left Ctrl Key)
0x09, 0xe2,                 // USAGE (Left Alt Key)
0x09, 0xe3,                 // USAGE (Left Windows Key)
0x15, 0x00,                 // LOGICAL_MINIMUM (0)
0x25, 0x01,                 // LOGICAL_MAXIMUM (1)
0x75, 0x01,                 // REPORT_SIZE (1)
0x95, 0x06,                 // REPORT_COUNT (5)
0x81, 0x02,                 // INPUT (Data, Var, Abs)
0x95, 0x1a,                 // REPORT_COUNT (27)
0x81, 0x03,                 // INPUT (Cnst, Var, Abs)
0xc0,                          // END_COLLECTION
    
0x05, 0x0C,          // USAGE_PAGE (Consumer devices)
0x09, 0x01,          // USAGE (Consumer Control)
0xa1, 0x01,          // COLLECTION (Application)
0x85, REPORTID_VOLUME, // REPORT_ID
0x09, 0xe9,              // USAGE (Volume up)
0x09, 0xea,              // USAGE (Volume down)
0x15, 0x00,          // LOGICAL_MINIMUM (0)
0x25, 0x01,          // LOGICAL_MAXIMUM (1)
0x75, 0x01,              // REPORT_SIZE (1)
0x95, 0x02,              // REPORT_COUNT (2)
0x81, 0x02,              // INPUT (Data, Var, Abs)
0x95, 0x1e,              // REPORT_COUNT (30)
0x81, 0x03,          // INPUT (Cnst, Var, Abs)
0xc0,                   // END_COLLECTION
    
0x05, 0x01,             // USAGE_PAGE (Generic Desktop)
0x09, 0x80,             // USAGE (System Control)
0xa1, 0x01,             // COLLECTION (Application)
0x85, REPORTID_POWER, // REPORT_ID
0x09, 0x81,             // USAGE (System power down)
0x09, 0x83,             // USAGE (System wake up)
0x15, 0x00,             // LOGICAL_MINIMUM (0)
0x25, 0x01,             // LOGICAL_MAXIMUM (1)
0x75, 0x01,             // REPORT_SIZE (1)
0x95, 0x02,             // REPORT_COUNT (2)
0x81, 0x02,             // INPUT (Data,Var,Abs)
0x95, 0x1e,             // REPORT_COUNT (30)
0x81, 0x03,             // INPUT (Cnst,Var,Abs)
0xc0,           // END_COLLECTION
```

 

 




