---
title: 在 WIA 驱动程序中启用 TWAIN 功能传递
description: 在 WIA 驱动程序中启用 TWAIN 功能传递
ms.assetid: b2108109-9e41-481d-bc25-67327420faf9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49a79ddc3846d23fbc6e20da11e8c50144557c11
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364431"
---
# <a name="enabling-twain-capability-pass-through-in-a-wia-driver"></a>在 WIA 驱动程序中启用 TWAIN 功能传递





若要启用对 TWAIN 功能传递的支持，请添加**WiaItemTypeTwainCapabilityPassThrough**标记，用于[ **WIA\_IPA\_项\_标志**](https://msdn.microsoft.com/library/windows/hardware/ff551585)根项上的属性。 头文件中定义此标志*wiatwcmp.h*。

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

 

 




