---
title: 显示驱动程序的同步问题
description: 显示驱动程序的同步问题
ms.assetid: 7d87e963-02c3-4da2-9dbd-ca14bde2867b
keywords:
- 显示驱动程序 WDK Windows 2000 中，同步
- 同步 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67f6585c9318b199a947e240d8d8b585b1d0ff78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569326"
---
# <a name="synchronization-issues-for-display-drivers"></a>显示驱动程序的同步问题


Microsoft 建议显示器驱动程序在持有锁不调用任何 GDI 函数。 这一点尤其重要，显示器驱动程序不会调用任意以下函数时持有互斥锁。 执行此操作可能会导致死锁。

-   BRUSHOBJ\_hGetColorTransform

-   BRUSHOBJ\_pvAllocRbrush

-   BRUSHOBJ\_pvGetRbrush

-   BRUSHOBJ\_ulGetBrushColor

-   CLIPOBJ\_bEnum

-   CLIPOBJ\_cEnumStart

-   CLIPOBJ\_ppoGetPath

-   EngAcquireSemaphore

-   EngAllocMem

-   EngAllocPrivateUserMem

-   EngAllocUserMem

-   EngAlphaBlend

-   EngAssociateSurface

-   EngBitBlt

-   EngCheckAbort

-   EngComputeGlyphSet

-   EngControlSprites

-   EngCopyBits

-   EngCreateBitmap

-   EngCreateClip

-   EngCreateDeviceBitmap

-   EngCreateDeviceSurface

-   EngCreateDriverObj

-   EngCreateEvent

-   EngCreatePalette

-   EngCreatePath

-   EngCreateSemaphore

-   EngCreateWnd

-   EngDeleteClip

-   EngDeleteDriverObj

-   EngDeleteEvent

-   EngDeletePalette

-   EngDeletePath

-   EngDeleteSafeSemaphore

-   EngDeleteSemaphore

-   EngDeleteSurface

-   EngDeleteWnd

-   EngDxIoctl

-   EngEraseSurface

-   EngFillPath

-   EngFntCacheAlloc

-   EngFntCacheFault

-   EngFntCacheLookUp

-   EngFreeMem

-   EngFreeModule

-   EngFreePrivateUserMem

-   EngFreeUserMem

-   EngGetType1FontList

-   EngGradientFill

-   EngHangNotification

-   EngInitializeSafeSemaphore

-   EngLineTo

-   EngLoadImage

-   EngLoadModule

-   EngLoadModuleForWrite

-   EngLockDirectDrawSurface

-   EngLockDriverObj

-   EngLockSurface

-   EngMapEvent

-   EngMapFile

-   EngMapFontFileFD

-   EngMarkBandingSurface

-   EngModifySurface

-   EngMovePointer

-   EngNineGrid

-   EngPaint

-   EngPlgBlt

-   EngQueryPalette

-   EngReleaseSemaphore

-   EngSetPointerShape

-   EngStretchBlt

-   EngStretchBltROP

-   EngStrokeAndFillPath

-   EngStrokePath

-   EngTextOut

-   EngTransparentBlt

-   EngUnloadImage

-   EngUnlockDirectDrawSurface

-   EngUnlockDriverObj

-   EngUnlockSurface

-   EngUnmapEvent

-   EngUnmapFile

-   EngUnmapFontFile

-   EngUnmapFontFileFD

-   EngWaitForSingleObject

-   FONTOBJ\_cGetAllGlyphHandles

-   FONTOBJ\_cGetGlyphs

-   FONTOBJ\_pifi

-   FONTOBJ\_pjOpenTypeTablePointer

-   FONTOBJ\_pQueryGlyphAttrs

-   FONTOBJ\_pvTrueTypeFontFile

-   FONTOBJ\_pxoGetXform

-   FONTOBJ\_vGetInfo

-   HeapVidMemAllocAligned

-   PALOBJ\_cGetColors

-   PATHOBJ\_bEnumClipLines

-   PATHOBJ\_bMoveTo

-   PATHOBJ\_bPolyBezierTo

-   PATHOBJ\_vEnumStartClipLines

-   PATHOBJ\_vGetBounds

-   STROBJ\_bEnum

-   VidMemFree

-   WNDOBJ\_bEnum

-   WNDOBJ\_cEnumStart

-   WNDOBJ\_vSetConsumer

-   XFORMOBJ\_bApplyXform

-   XFORMOBJ\_iGetFloatObjXform

-   XFORMOBJ\_iGetXform

-   XLATEOBJ\_cGetPalette

-   XLATEOBJ\_hGetColorTransform

-   XLATEOBJ\_iXlate

-   XLATEOBJ\_piVector

 

 





