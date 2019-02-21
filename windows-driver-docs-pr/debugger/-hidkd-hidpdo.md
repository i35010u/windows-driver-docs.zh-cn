---
title: hidkd.hidpdo
description: Hidkd.hidpdo 命令显示与物理设备对象 (PDO) 相关联的 HID 信息。
ms.assetid: B7FF3B62-AC41-4CFC-A9D6-609B1204E4CA
keywords:
- hidkd.hidpdo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- hidkd.hidpdo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3cc6d6bec5d6ff8bdd59bcf6344cdc8be7f7bcfb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525475"
---
# <a name="hidkdhidpdo"></a>!hidkd.hidpdo


**！ Hidkd.hidpdo**命令将显示与物理设备对象 (PDO) 相关联的 HID 信息。

```dbgcmd
!hidkd.hidpdo pdo
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______pdo______"></span><span id="_______PDO______"></span> *pdo*   
PDO 的地址。 若要获取 PDOs 与 HID 驱动程序相关联的地址，请使用[ **！ usbhid.hidtree** ](-hidkd-hidtree.md)命令。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Hidkd.dll

<a name="examples"></a>示例
--------

下面是输出的示例 **！ hidpdo**命令。 此示例首先调用[ **！ hidtree** ](-hidkd-hidtree.md)获取 PDO 的地址。

```dbgcmd
0: kd> !hidkd.hidtree
HID Device Tree
...
FDO  VendorID:0x045E(Microsoft Corporation) ProductID:0x0745 Version:0x0634
...
    PDO  Generic Desktop Controls (0x01) | Mouse (0x02)
    !hidpdo 0xffffe000056281e0
    ...

0: kd> !hidpdo 0xffffe000056281e0
# PDO 0xffffe000056281e0  (!devobj/!devstack)

  Collection Num  : 1
  Name            : \Device\_HID00000002#COLLECTION00000001
  FDO             : !hidfdo 0xffffe00004f466e0
  Per-FDO IFR Log : !rcdrlogdump HIDCLASS -a 0xFFFFE0000594D000

  Usage Page      : Generic Desktop Controls (0x01)
  Usage           : Mouse (0x02)
  Report Length   : 0xa(Input) 0x0(Output) 0x2(Feature)
  Pre-parsed Data : 0xffffe00003742840
  Position in HID tree

  dt PDO_EXTENSION 0xffffe00005628350

## Power States

  Power States  : S0/D0
  Wait Wake IRP : !irp 0xffffe00004fc57d0 (pending on \Driver\HidUsb)
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[HID 的扩展](hid-extensions.md)

 

 






