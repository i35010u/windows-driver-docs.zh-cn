---
title: 显示驱动程序的同步问题
description: 显示驱动程序的同步问题
keywords:
- 显示驱动程序 WDK Windows 2000，同步
- 同步 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c8691295f22e2b34885c1da7d3c11e06f9065f7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838949"
---
# <a name="synchronization-issues-for-display-drivers"></a>显示驱动程序的同步问题


Microsoft 建议显示驱动程序在持有锁时不调用任何 GDI 函数。 尤其重要的是，显示驱动程序在保存互斥体时不调用任何以下函数。 这样做可能会导致死锁。

-   BRUSHOBJ \_ hGetColorTransform

-   BRUSHOBJ \_ pvAllocRbrush

-   BRUSHOBJ \_ pvGetRbrush

-   BRUSHOBJ \_ ulGetBrushColor

-   CLIPOBJ \_ bEnum

-   CLIPOBJ \_ cEnumStart

-   CLIPOBJ \_ ppoGetPath

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

-   FONTOBJ \_ cGetAllGlyphHandles

-   FONTOBJ \_ cGetGlyphs

-   FONTOBJ \_ pifi

-   FONTOBJ \_ pjOpenTypeTablePointer

-   FONTOBJ \_ pQueryGlyphAttrs

-   FONTOBJ \_ pvTrueTypeFontFile

-   FONTOBJ \_ pxoGetXform

-   FONTOBJ \_ vGetInfo

-   HeapVidMemAllocAligned

-   PALOBJ \_ cGetColors

-   PATHOBJ \_ bEnumClipLines

-   PATHOBJ \_ bMoveTo

-   PATHOBJ \_ bPolyBezierTo

-   PATHOBJ \_ vEnumStartClipLines

-   PATHOBJ \_ vGetBounds

-   STROBJ \_ bEnum

-   VidMemFree

-   WNDOBJ \_ bEnum

-   WNDOBJ \_ cEnumStart

-   WNDOBJ \_ vSetConsumer

-   XFORMOBJ \_ bApplyXform

-   XFORMOBJ \_ iGetFloatObjXform

-   XFORMOBJ \_ iGetXform

-   XLATEOBJ \_ cGetPalette

-   XLATEOBJ \_ hGetColorTransform

-   XLATEOBJ \_ iXlate

-   XLATEOBJ \_ piVector

 

 





