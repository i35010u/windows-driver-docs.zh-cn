---
title: 如何实现扩展的相机控件属性
description: 照相机的驱动程序实现扩展的照相机控件属性。
ms.assetid: BF5B2F1F-AC1D-4ED1-B1FC-64E8FA1218DA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df91e1cef783dc6e70bd43c4505c7aaee426e48b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363501"
---
# <a name="how-to-implement-extended-camera-control-properties"></a>如何实现扩展的相机控件属性


照相机的驱动程序应实现[扩展相机控件属性](extended-camera-control-properties.md)作为单个属性设置 — 也就是说，每个属性应作为单个属性集。 下面的示例代码可以用于实现这些属性使用作为起始点。

**请注意**  扩展的属性的数据大小可以是任意长度，因为缓冲区为空表示通过查询数据的大小在用户模式堆栈。 需要一个两步过程： 首先驱动程序将返回所需的长度，如代码示例中所示，然后在用户模式堆栈请求属性数据的正确缓冲区。

 

## <a name="driver-implementation"></a>驱动程序实现


```cpp
DEFINE_KSPROPERTY_TABLE(SocSimFilterFocusPropertyItems)
{       
    DEFINE_KSPROPERTY_ITEM(
        0,
        CCaptureFilter::FocusRectHandler,
        sizeof(KSPROPERTY),
        0,
        CCaptureFilter::FocusRectHandler,
        NULL, 0, NULL, NULL, 0
        )
};

DEFINE_KSPROPERTY_TABLE(SocSimFilterVideoStabPropertyItems)
{       
    DEFINE_KSPROPERTY_ITEM(
        0,
        CCaptureFilter::VideoStabilizationModeHandler,
        sizeof(KSPROPERTY),
        0,
        CCaptureFilter::VideoStabilizationModeHandler,
        NULL, 0, NULL, NULL, 0
        )
};

DEFINE_KSPROPERTY_TABLE(SocSimFilterFlashPropertyItems)
{       
    DEFINE_KSPROPERTY_ITEM(
        0,
        CCaptureFilter::FlashHandler,
        sizeof(KSPROPERTY),
        0,
        CCaptureFilter::FlashHandler,
        NULL, 0, NULL, NULL, 0
        )
};

DEFINE_KSPROPERTY_SET_TABLE(SocSimFilterPropertySets)
{
    DEFINE_KSPROPERTY_SET(
        &PROPSETID_VIDCAP_CAMERACONTROL_REGION_OF_INTEREST,
        SIZEOF_ARRAY(SocSimFilterFocusPropertyItems),
        SocSimFilterFocusPropertyItems,
        0,
        NULL),

    DEFINE_KSPROPERTY_SET(
        &PROPSETID_VIDCAP_CAMERACONTROL_FLASH,
        SIZEOF_ARRAY(SocSimFilterFlashPropertyItems),
        SocSimFilterFlashPropertyItems,
        0,
        NULL),

    DEFINE_KSPROPERTY_SET(
        &PROPSETID_VIDCAP_CAMERACONTROL_VIDEO_STABILIZATION,
        SIZEOF_ARRAY(SocSimFilterVideoStabPropertyItems),
        SocSimFilterVideoStabPropertyItems,
        0,
        NULL)

};

NTSTATUS
CCaptureFilter::FlashHandler(
    __in    PIRP Irp,
    __in    PKSPROPERTY Property,
    __inout PVOID pData
    )
{
    PAGED_CODE();
    NTSTATUS Status = STATUS_SUCCESS;
    NT_ASSERT(Irp);
    NT_ASSERT(Property);

    CCaptureFilter* pFilter = reinterpret_cast <CCaptureFilter*>(KsGetFilterFromIrp(Irp)->Context);

    PIO_STACK_LOCATION pIrpStack = IoGetCurrentIrpStackLocation(Irp);
    ULONG ulOutputBufferLength = pIrpStack->Parameters.DeviceIoControl.OutputBufferLength;
    ULONG InputBufferLength = pIrpStack->Parameters.DeviceIoControl.InputBufferLength;

    if (Property->Flags & KSPROPERTY_TYPE_SET)
    {
        if (ulOutputBufferLength == 0)
        {
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S);
            Status = STATUS_BUFFER_OVERFLOW;
        }
        else if (ulOutputBufferLength < sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S))
        {
            Status = STATUS_BUFFER_TOO_SMALL;
        }
        else if (pData && ulOutputBufferLength >= sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S))
        {
            PKSPROPERTY_CAMERACONTROL_FLASH_S pFlash = (PKSPROPERTY_CAMERACONTROL_FLASH_S)pData;
            pFilter->m_Flash = pFlash->Flash;
            pFilter->m_FlashCapabilites = pFlash->Capabilities;
            Status = STATUS_SUCCESS;
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S);
        }
        else 
        {
            Status = STATUS_INVALID_PARAMETER;
        }
    }
    else if (Property->Flags & KSPROPERTY_TYPE_GET)
    {
        if (ulOutputBufferLength == 0)
        {
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S);
            Status = STATUS_BUFFER_OVERFLOW;
        }
        else if (ulOutputBufferLength < sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S))
        {
            Status = STATUS_BUFFER_TOO_SMALL;
        }
        else if (pData && ulOutputBufferLength >= sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S))
        {
            PKSPROPERTY_CAMERACONTROL_FLASH_S pFlash = (PKSPROPERTY_CAMERACONTROL_FLASH_S)pData;
            pFlash->Flash = pFilter->m_Flash;
            pFlash->Capabilities = pFilter->m_FlashCapabilites;
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S);
            Status = STATUS_SUCCESS;
        }
        else
        {
            Status = STATUS_INVALID_PARAMETER;
        }
    }

    return Status;
}

NTSTATUS
CCaptureFilter::VideoStabilizationModeHandler(
    __in    PIRP Irp,
    __in    PKSPROPERTY Property,
    __inout PVOID pData
    )
{
    PAGED_CODE();
    NTSTATUS Status = STATUS_SUCCESS;
    NT_ASSERT(Irp);
    NT_ASSERT(Property);

    CCaptureFilter* pFilter = reinterpret_cast <CCaptureFilter*>(KsGetFilterFromIrp(Irp)->Context);

    PIO_STACK_LOCATION pIrpStack = IoGetCurrentIrpStackLocation(Irp);
    ULONG ulOutputBufferLength = pIrpStack->Parameters.DeviceIoControl.OutputBufferLength;
    ULONG InputBufferLength = pIrpStack->Parameters.DeviceIoControl.InputBufferLength;

    if (Property->Flags & KSPROPERTY_TYPE_SET)
    {
        if (ulOutputBufferLength == 0)
        {
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S);
            Status = STATUS_BUFFER_OVERFLOW;
        }
        else if (ulOutputBufferLength < sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S))
        {
            Status = STATUS_BUFFER_TOO_SMALL;
        }
        else if (pData && ulOutputBufferLength >= sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S))
        {
            PKSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S pVideoStab = (PKSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S)pData;
            pFilter->m_VideoStabMode = pVideoStab->VideoStabilizationMode;
            pFilter->m_VideoStabCapabilites = pVideoStab->Capabilities;
            Status = STATUS_SUCCESS;
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S);
        }
        else 
        {
            Status = STATUS_INVALID_PARAMETER;
        }
    }
    else if (Property->Flags & KSPROPERTY_TYPE_GET)
    {
        if (ulOutputBufferLength == 0)
        {
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S);
            Status = STATUS_BUFFER_OVERFLOW;
        }
        else if (ulOutputBufferLength < sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S))
        {
            Status = STATUS_BUFFER_TOO_SMALL;
        }
        else if (pData && ulOutputBufferLength >= sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S))
        {
            PKSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S pVideoStab = (PKSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S)pData;
            pVideoStab->VideoStabilizationMode = pFilter->m_VideoStabMode;
            pVideoStab->Capabilities = pFilter->m_VideoStabCapabilites;
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S);
            Status = STATUS_SUCCESS;
        }
        else
        {
            Status = STATUS_INVALID_PARAMETER;
        }
    }

    return Status;
}

NTSTATUS
CCaptureFilter::FocusRectHandler(
    __in    PIRP Irp,
    __in    PKSPROPERTY Property,
    __inout PVOID pData
    )
{
    PAGED_CODE();
    NTSTATUS Status = STATUS_SUCCESS;
    NT_ASSERT(Irp);
    NT_ASSERT(Property);

    CCaptureFilter* pFilter = reinterpret_cast <CCaptureFilter*>(KsGetFilterFromIrp(Irp)->Context);

    PIO_STACK_LOCATION pIrpStack = IoGetCurrentIrpStackLocation(Irp);
    ULONG ulOutputBufferLength = pIrpStack->Parameters.DeviceIoControl.OutputBufferLength;
    ULONG InputBufferLength = pIrpStack->Parameters.DeviceIoControl.InputBufferLength;

    if (Property->Flags & KSPROPERTY_TYPE_SET)
    {
        if (ulOutputBufferLength == 0)
        {
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S);
            Status = STATUS_BUFFER_OVERFLOW;
        }
        else if (ulOutputBufferLength < sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S))
        {
            Status = STATUS_BUFFER_TOO_SMALL;
        }
        else if (pData && ulOutputBufferLength >= sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S))
        {
            PKSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S pFocusRect = (PKSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S)pData;
            pFilter->m_FocusRect.left = pFocusRect->FocusRect.left;
            pFilter->m_FocusRect.top = pFocusRect->FocusRect.top;
            pFilter->m_FocusRect.right = pFocusRect->FocusRect.right;
            pFilter->m_FocusRect.bottom = pFocusRect->FocusRect.bottom;
            pFilter->m_AutoFocusLock = pFocusRect->AutoFocusLock;
            pFilter->m_AutoExposureLock = pFocusRect->AutoExposureLock;
            pFilter->m_AutoWhitebalanceLock = pFocusRect->AutoWhitebalanceLock;
            Status = STATUS_SUCCESS;
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S);
        }
        else 
        {
            Status = STATUS_INVALID_PARAMETER;
        }
    }
    else if (Property->Flags & KSPROPERTY_TYPE_GET)
    {
        if (ulOutputBufferLength == 0)
        {
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S);
            Status = STATUS_BUFFER_OVERFLOW;
        }
        else if (ulOutputBufferLength < sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S))
        {
            Status = STATUS_BUFFER_TOO_SMALL;
        }
        else if (pData && ulOutputBufferLength >= sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S))
        {
            PKSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S pFocusRect = (PKSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S)pData;
            pFocusRect->FocusRect.left = pFilter->m_FocusRect.left;
            pFocusRect->FocusRect.top = pFilter->m_FocusRect.top;
            pFocusRect->FocusRect.right = pFilter->m_FocusRect.right;
            pFocusRect->FocusRect.bottom = pFilter->m_FocusRect.bottom;
            pFocusRect->AutoFocusLock = pFilter->m_AutoFocusLock;
            pFocusRect->AutoExposureLock = pFilter->m_AutoExposureLock;
            pFocusRect->AutoWhitebalanceLock = pFilter->m_AutoWhitebalanceLock;
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S);
            Status = STATUS_SUCCESS;
        }
        else
        {
            Status = STATUS_INVALID_PARAMETER;
        }
    }

    return Status;
}
```

 

 




