---
title: hidkd.hidfdo
description: Hidkd.hidfdo 命令显示 HID 信息与功能的设备对象 (FDO) 相关联。
ms.assetid: CB8E8844-B5A7-4273-8401-D4F3C8CBAC4C
keywords:
- hidkd.hidfdo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- hidkd.hidfdo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bd543510a68f1455ef54fa71376a5eeedaf7ee24
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522040"
---
# <a name="hidkdhidfdo"></a>!hidkd.hidfdo


**！ Hidkd.hidfdo**命令显示 HID 信息与功能的设备对象 (FDO) 相关联。

```dbgcmd
!hidkd.hidfdo fdo
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______fdo______"></span><span id="_______FDO______"></span> *fdo*   
FDO 的地址。 若要获取 FDOs 与 HID 驱动程序相关联的地址，请使用[ **！ usbhid.hidtree** ](-hidkd-hidtree.md)命令。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Hidkd.dll

<a name="examples"></a>示例
--------

下面是输出的示例 **！ hidfdo**命令。 此示例首先调用[ **！ hidtree** ](-hidkd-hidtree.md)获取 FDO 的地址。

```dbgcmd
0: kd> !hidkd.hidtree
HID Device Tree
...
FDO  VendorID:0x045E(Microsoft Corporation) ProductID:0x0745 Version:0x0634
!hidfdo 0xffffe00004f466e0
...
0: kd> !hidfdo 0xffffe00004f466e0
# FDO 0xffffe00004f466e0  (!devobj/!devstack)

  Name              : \Device\_HID00000002
  Vendor ID         : 0x045E(Microsoft Corporation)
  Product ID        : 0x0745
  Version Number    : 0x0634
  Is Present?       : Y
  Report Descriptor : !hidrd 0xffffe00004281a80 0x127
  Per-FDO IFR Log   : !rcdrlogdump HIDCLASS -a 0xFFFFE0000594D000

  Position in HID tree

  dt FDO_EXTENSION 0xffffe00004f46850
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[HID 的扩展](hid-extensions.md)

 

 






