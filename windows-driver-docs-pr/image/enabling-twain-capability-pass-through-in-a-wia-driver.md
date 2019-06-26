---
title: 在 WIA 驱动程序中启用 TWAIN 功能传递
description: 在 WIA 驱动程序中启用 TWAIN 功能传递
ms.assetid: b2108109-9e41-481d-bc25-67327420faf9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1371c590edfce629bb67291d4bb486e54402d77
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385027"
---
# <a name="enabling-twain-capability-pass-through-in-a-wia-driver"></a>在 WIA 驱动程序中启用 TWAIN 功能传递





若要启用对 TWAIN 功能传递的支持，请添加**WiaItemTypeTwainCapabilityPassThrough**标记，用于[ **WIA\_IPA\_项\_标志**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-flags)根项上的属性。 头文件中定义此标志*wiatwcmp.h*。

下面的示例取自*wiascanr*示例 (包括在驱动程序开发工具包\[DDK\]) 并演示如何使用**WiaItemTypeTwainCapabilityPassThrough**标志)。

```cpp
// Initialize WIA_IPA_ITEM_FLAGS
  m_pszRootItemDefaults[PropIndex] = WIA_IPA_ITEM_FLAGS_STR;
  m_piRootItemDefaults[PropIndex] = WIA_IPA_ITEM_FLAGS;
// Next assignment adds the WiaItemTypeTwainCapabilityPassThrough flag.
  m_pvRootItemDefaults[PropIndex].lVal = 
     WiaItemTypeRoot|WiaItemTypeFolder | 
     WiaItemTypeDevice| WiaItemTypeTwainCapabilityPassThrough;
  m_pvRootItemDefaults[PropIndex].vt = VT_I4;
  m_psRootItemDefaults[PropIndex].ulKind = PRSPEC_PROPID;
  m_psRootItemDefaults[PropIndex].propid = 
     m_piRootItemDefaults[PropIndex];
  m_wpiRootItemDefaults[PropIndex].lAccessFlags = 
     WIA_PROP_READ | WIA_PROP_FLAG;
  m_wpiRootItemDefaults[PropIndex].vt = 
     m_pvRootItemDefaults [PropIndex].vt;
  m_wpiRootItemDefaults[PropIndex].ValidVal.Flag.Nom = 
     m_pvRootItemDefaults [PropIndex].lVal;
  m_wpiRootItemDefaults[PropIndex].ValidVal.Flag.ValidBits = 
     WiaItemTypeRoot | WiaItemTypeFolder|WiaItemTypeDevice;
```

 

 




