---
title: 在 WIA 驱动程序中启用 TWAIN 功能传递
description: 在 WIA 驱动程序中启用 TWAIN 功能传递
ms.assetid: b2108109-9e41-481d-bc25-67327420faf9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91567697ebb7500df15743952fd3cf41affc2ad7
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192287"
---
# <a name="enabling-twain-capability-pass-through-in-a-wia-driver"></a>在 WIA 驱动程序中启用 TWAIN 功能传递





若要启用对 TWAIN 功能传递的支持，请将 **WiaItemTypeTwainCapabilityPassThrough** 标志添加到根项的 [**WIA \_ IPA \_ 项 \_ FLAGS**](./wia-ipa-item-flags.md) 属性中。 此标志在头文件 *wiatwcmp*中定义。

下面的示例摘自驱动程序开发工具包 DDK 中包含的 *wiascanr* 示例 (\[ \] ，) 并演示了如何使用 **WiaItemTypeTwainCapabilityPassThrough** 标志) 。

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

 

