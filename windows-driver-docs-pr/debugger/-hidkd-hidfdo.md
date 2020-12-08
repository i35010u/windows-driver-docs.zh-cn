---
title: hidkd.hidfdo
description: Hidkd. hidfdo 命令显示与功能设备对象 (FDO) 相关联的 HID 信息。
keywords:
- hidkd hidfdo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- hidkd.hidfdo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8ceded47650c141a5acff0dc48c7c1aff6a1fbec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825839"
---
# <a name="hidkdhidfdo"></a>!hidkd.hidfdo


**！ Hidkd hidfdo** 命令显示与功能设备对象相关联 (FDO) 的 HID 信息。

```dbgcmd
!hidkd.hidfdo fdo
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______fdo______"></span><span id="_______FDO______"></span>*fdo*   
FDO 的地址。 若要获取与 HID 驱动程序相关联的 FDOs 的地址，请使用 [**！ usbhid. hidtree**](-hidkd-hidtree.md) 命令。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Hidkd.dll

<a name="examples"></a>示例
--------

下面是 **！ hidfdo** 命令的输出示例。 该示例首先调用 [**！ hidtree**](-hidkd-hidtree.md) 以获取 FDO 的地址。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HID 扩展](hid-extensions.md)

 

 






